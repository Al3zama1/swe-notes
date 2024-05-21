## The Purpose of DHCP
* DHCP is used to allow hosts to automatically/dynamically learn various aspects of their network configuration, such as IP addresses, subnet mask, default gateway, DNS server, etc, without manual/static configuration.
* It is an essential part of modern networks.
* Typically used for 'client devices' such as workstations (PCs), phones, etc.
* Devices such as routers, servers, etc, are usually manually configured.
* In small networks (such as home networks) the router typically acts as the DHCP server for hosts in the LAN.
* In larger networks, the DHCP server is usually a Windows/Linux server.
## Basic Function of DHCP

### Release IP
```
ipconfig /release
```
* The device releases the assigned IP address (windows).
* The device sends a DHCP release message to the DHCP server, setting it that the IP address isn't needed anymore.
	* The IP becomes available and can be assigned to another client.
### Get IP Address from DHCP Server
```
ipconfig /renew
```
* This process involves 4 messages
### DHCP Messages
![DHCP message types](./img3/dhcp-message-types.png)
#### DHCP Discover
* It is a broadcast message from the client asking if there is any DHCP servers in the local network.
#### DHCP Offer
* It is sent from the DHCP server to the client, offering an address for the client to use, as well as other information like default gateway, DNS server, etc.
#### DHCP Request
* It is sent from the DHCP client to the server, telling the server that it wants to use the IP address it was offered.
* This is important, there may be multiple DHCP servers on the local network, and all of them will reply to the client's Discover message with an offer. Therefore, the client has to specify which server it is accepting the offer from and request to use that IP address.
	* Typically, the client will accept the first offer it receives.
#### DHCP Ack
* Sent from the server to the client, confirming that the client may use the requested IP address.
* Once the message is received, the client configures the IP address on its network interface
### DHCP Relay
![DHCP relay](./img3/dhcp-relay.png)
* Some network engineers might choose to configure each router to act as the DHCP server for its connected LANs.
* However, large enterprises often choose to use a centralized DHCP server.
* If the server is centralized, it won't receive the DHCP clients' broadcast DHCP messages (broadcast messages don't leave the local subnet).
* To fix this, you can configure a router to act as a **DHCP relay agent**.
* The router will then forward the client's broadcast DHCP messages to the remove DHCP server as unicast messages.
## Configuring DHCP in Cisco IOS

### Router DHCP Server Configuration
![Router DHCP configuration](./img3/router-dhcp-server-config.png)

```
R1(config)#ip dhcp excluded-address 192.168.1.1 192.168.1.10
```
* Specify a range of addresses that won't be given to DHCP clients. The first address is the start of the range and the second address is the end of the range.
* These are addresses you want to reserve for network devices or servers in the local subnet.

```
R1(config)#ip dhcp pool LAB_POOL
R1(dhcp-config)#network 192.168.1.0 ?
```
* Create a DHCP pool, which is a subnet of addresses that can be assigned to DHCP clients, as well as other info such as DNS server and default gateway.
* You should create a separate DHCP pool for each network the router is acting as a DHCP server for.
	* In this case R1 is only acting as the DHCP server for `192.168.1.0/24`, so only one DHCP pool needed to be created.
