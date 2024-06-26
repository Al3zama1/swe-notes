## Another way To Configure Numbered ACLs
* This applies to both Standard and Extended Numbered ACLs.
* Numbered ACLs are configured in global config mode:
	* `R1(config)#access-list 1 deny 192.168.1.1`
	* `R1(config)#access-list 1 permit any`
* Named ACLs are configured with subcommands in a separate config mode:
	* `R1(config)#ip access-list standard BLOCK_PC1`
	* `R1(config-std-nacl)#deny 192.168.1.1`
	* `R1(config-std-nacl)#permit any`
* However, in modern IOS you can also configure numbered ACLs in the exact same way as named ACLs:
	* `R1(config)#ip access-list standard 1`
	* `R1(config-std-nacl)#deny 192.168.1.1`
	* `R1(config-std-nacl)#permit any`
	* This is just a different way of configuring numbered ACLs. However, in the running-config the ACL will display as if it was configured using the traditional method from global config mode.
## Editing ACLs
### Advantages of Named ACL Config Mode
```
R1(config-std-nacl)#do show access-lists
Standard IP access list 1
	10 deny 192.168.1.1
	20 deny 192.168.1.2
	30 deny 192.168.3.0, wildcard bits 0.0.0.255
	40 permit any
	
R1(config-std-nacl)#no 30

R1(config-std-nacl)#do show access-lists
Standard IP access list 1
	10 deny 192.168.1.1
	20 deny 192.168.1.2
	40 permit any
```
* You can easily delete individual entries in the ACL with `no entry-number`.
	* **On the other hand, when configuring/editing numbered ACLs from global config mode, you can't delete individual entries, you can only delete the entire ACL.**
	* If you want to edit it, you have to delete it and then remake it from scratch.
	* It is possible to configure a numbered ACL in global config mode, and then just use named ACL config mode when you need to edit the ACL.

```
R1(config-std-nacl)#do show access-lists
Standard IP access list 1
	10 deny 192.168.1.1
	20 deny 192.168.1.2
	40 permit any

R1(config-std-nacl)#30 deny 192.168.2.0 0.0.0.255

R1(config-std-nacl)#do show access-lists
Standard IP access list 1
	10 deny 192.168.1.1
	20 deny 192.168.1.2
	30 deny 192.168.2.0, wildcard bits 0.0.0.255
	40 permit any
```
* You can insert new entries in between other entries by specifying the sequence number.
	* When configuring an ACL from global config mode, you can't specify the sequence number. The entry is simply added to the end of the ACL and the sequence number is automatically set to 10 higher than the current highest sequence number.
### Resequencing ACLs
Resequencing ACLs is a function that helps edit ACLs.
```
R1(config)#ip access-list resequence acl-id starting-seq-num increment
```
* `acl-id` can be a number or name depending on whether a named or numbered ACL was used.
* The command works for all ACLs.


```
R1(config)#do show access-lists
Standard IP access list 1
	1 deny 192.168.1.1
	3 deny 192.168.3.1
	2 deny 192.168.2.1
	4 deny 192.168.4.1
	5 permit any
```
* The way the entries in the ACL are configured with their sequence numbers, makes it impossible to insert an entry in between the other entries.

```
R1(config)#ip access-list resequence 1 10 10

R1(config)#do show access-lists
Standard IP access list 1
	10 deny 192.168.1.1
	20 deny 192.168.3.1
	30 deny 192.168.2.1
	40 deny 192.168.4.1
	50 permit any
```
* Now it's simple to add new entries in between the current entries.
## Extended Numbered & Named ACLs
* Extended ACLs function mostly the same as standard ACLs.
* They can be numbered or named, just like standard ACLs.
	* Numbered ACLs use the following ranges: 100 - 199, 2000 - 2699.
* They are processed from top to bottom, just like standard ACLs.
* They can match traffic based on more parameters, so they are more precise and more complex than ACLs.
* Extended ACLs should be applied as close to the source as possible, to limit how far the packets travel in the network before being denied.
	* On the other hand, standard ACLs are less specific, so if they are applied close to the source, there is a risk of blocking more traffic than intended. Therefore, they are applied as close to the destination as possible
* We will focus on matching based on these main parameters: 
	* Layer 4 protocol/port.
	* Source IP address.
	* Destination IP address.

### Configuration
#### Configure Extended Numbered ACLs
```
R1(config)#access-list number [permit | deny] protocol src-ip dest-ip
```
#### Configure Extended Named ACLs
```
R1(config)#ip access-list extended {name | number}
R1(config-ext-nacl)#[sequence-num] {permit | deny} protocol src-ip dest-ip
```

### Extended ACL Match Based on Protocol
```
Router(config-ext-nacl)#deny ?
ahp   Authentication Header Protocol
eigrp Cisco's EIGRP routing protocol
esp   Encapsulation Security Payload
gre   Cisco's GRE tunneling
icmp  Internet Control Message Protocol
ip    Any Internet Protocol
ospf  OSPF routing protocol
tcp   Transmission Control Protocol
udp   User Datagram Protocol
```
* We are going to focus on *TCP*, *UDP*, and *IP*.
* The *IP* option matches all IP packets. This option is used when we don't care about the protocol and just want to deny or permit all packets.
	* For example, if you want to put a 'permit any' statement at the end of an ACL, you would use the IP option.
### Matching the Source/Destination IP address
```
Router(config-ext-nacl)#deny tcp ?
A.B.C.D Source address
any     Any source host
host    A single source host

Router(config-ext-nacl)#deny tcp any 10.0.0.0 0.0.0.255
```
* Deny all packets that encapsulate a TCP segment, from any source, to destination 10.0.0.0/24
#### Examples
**Example 1**: Allow all traffic
```
`R1(config-ext-nacl)#permit ip any any`
```

**Example 2**: Prevent `10.0.0.0/16` from sending UDP traffic to `192.168.1.1/32`
```
R1(config-ext-nacl)#deny udp 10.0.0.0 0.0.255.255 host 192.168.1.1
```
* In extended ACLs, to specify a /32 source or destination you have to use the 'host' option or specify the wildcard mask. You can't just write the address without either of those.

**Example 3**: Prevent `172.16.1.1/32` from pinging hosts in `192.168.0.0/24`
```
R1(config-ext-nacl)#deny icmp host 172.16.1.1 192.168.0.0 0.0.0.255
```
### Matching the TCP/UDP Port Numbers
* When matching TCP/UDP, you can optionally specify the source and/or destination port numbers to match.
	* Specifying TCP or UDP without the port numbers, will match all port numbers.
```
R1(config-ext-nacl)#deny tcp src-ip <matcher> src-port-num dest-ip <matcher> dst-port-num
```
* The matcher can be:
	* eq: equal to.
	* gt: greater than.
	* lt: less than.
	* neq: not equal to.
	* range: between the ports specified.
* The most common choice is EQ, to match traffic for a specific port number.
* After the destination IP address and/or destination port numbers, there are many more options you can use to match (not necessary for the CCNA).
	* ack: match the TCP ACK flag.
	* fin: match the TCP FIN flag.
	* syn: match the TCP SYN flag.
	* ttl: match packets with a specific TTL value.
	* dscp: match packets with a specific DSCP (Differentiated Services Code Point) value.
* If you specify the protocol, source IP, source port, destination IP, destination port, etc, a packet must match all of those values to match the ACL entry. Even if it matches all except one of the parameters, the packet won't match that entry of the ACL.

```
R1(config-ext-nacl)#deny tcp any host 1.1.1.1 eq 80
```
* Deny all packets destined for IP address 1.1.1.1/32, TCP port 80.

#### Examples
**Example 1**: Allow traffic from `10.0.0.0/16` to access the server at `2.2.2.2/32` using HTTPS.
```
R1(config-ext-nacl)#permit TCP 10.0.0.0 0.0.255.255 host 2.2.2.2 eq 443
```

**Example 2**: Prevent all hosts using source UDP port numbers from 20000 to 30000 from accessing the server at `3.3.3.3/32`.
```
R1(config-ext-nacl)#deny UDP any range 20000 30000 host 3.3.3.3
```

**Example 3**: Allow hosts in `172.16.1.0/24` using a TCP source port greater than 9999 to access all TCP ports on server `4.4.4.4/32` except port 23.
```
R1(config-ext-nacl)#permit TCP 172.16.1.0 0.0.0.255 gt 9999 host 4.4.4.4 neq 23
```

### ACLs Configuration Based on Network Topology
![](./img2/standard-acls-topology.png)
**Requirements**:
* Hosts in `192.168.1.0/24` can't use HTTPS to access SRV1.
* Hosts in `192.168.2.0/24` can't access `10.0.2.0/24`
* None of the hosts in `192.168.1.0/24` or `192.168.2.0/24` can ping `10.0.1.0/24` or `10.0.2.0/24`.

```
R1(config)#ip access-list extended HTTP_SRV1
R1(config-ext-nacl)#deny tcp 192.168.1.0 0.0.0.255 host 10.0.1.100 eq 443
R1(config-ext-nacl)#permit ip any any
R1(config-ext-nacl)#interface g0/1
R1(config-if)#ip access-group HTTP_SRV1 in

R1(config)#ip access-list extended BLOCK_10.0.2.0/24
R1(config-ext-nacl)#deny ip 192.168.2.0 0.0.0.255 10.0.2.0 0.0.0.255
R1(config-ext-nacl)#permit ip any any
R1(config-ext-nacl)#interface g0/2
R1(config-if)#ip access-group BLOCK_10.0.2.0/24 in

R1(config)#ip access-list extended BLOCK_ICMP
R1(config-ext-nacl)#deny icmp 192.168.1.0 0.0.0.255 10.0.1.0 0.0.0.255
R1(config-ext-nacl)#deny icmp 192.168.1.0 0.0.0.255 10.0.2.0 0.0.0.255
R1(config-ext-nacl)#deny icmp 192.168.2.0 0.0.0.255 10.0.1.0 0.0.0.255
R1(config-ext-nacl)#deny icmp 192.168.2.0 0.0.0.255 10.0.2.0 0.0.0.255
R1(config-ext-nacl)#permit ip any any

// ACL applies to both 192.168.1.0/24, 192.168.2.0/24
R1(config-ext-nacl)#interface g0/0
R1(config-if)# ip access-group BLOCK_ICMP out
```
* ACL configuration can be quite flexible. Therefore, this is not the only solution that works.

**View ACLs Applied to an Interface**
`R1# show interface g0/0`
