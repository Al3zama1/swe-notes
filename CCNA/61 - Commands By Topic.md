## CLI Introduction
**Enter Privileged Exec Mode**
```
R1>enable
R1#
```
**Enter Global Configuration Mode**
```
R1#configure terminal
R1(config)#
```
**Enable Password**
```
// Sets password without ecryption
R1(config)#enable password

// Encrypt unencrypted passwords and future passwords
R1(config)#service password-encryption
```
* Sets type 7 encryption which is not secure.

```
R1(config)#no service password-encryption
```
* Will deactivate password encryption.
* Current encrypted passwords won't be decrypted.
**Enable Secret**
```
R1(config)#enable secret <secret>
```
* Sets MD5 type encryption.
**Show Configuration Files**
```
\\ Display device's running configuration
R1#show running-config

// Display device's startup configuration
R1#show startup-config
```
**Save Configuration File**
```
// Method 1
R1#write

// Method 2
R1#write memmory

// Method 3
R1#copy running-config startup-config
```
## Switch Interfaces
**Display MAC Address Table**
```
SW1#show mac address-table

Mac Address Table
-------------------------------------------

Vlan Mac Address Type Ports
---- ----------- -------- -----
1 0001.647b.3119 DYNAMIC Gig0/1
1 0004.9a6e.d870 DYNAMIC Gig0/1

SW1#
```
**Display Interface Brief**
```
SW1>enable
SW1#show ip interface brief
Interface       IP-Address     OK?     Method     Status    Protocol
FastEthernet0/1 unassigned     YES     unset      up        up
FastEthernet0/2 unassigned     YES     unset      down      down
```
**Display Interfaces Status**
```
Switch#show interfaces status

Port Name Status Vlan Duplex Speed Type

Fa0/1 connected 1 auto auto 10/100BaseTX
Fa0/2 notconnect 1 auto auto 10/100BaseTX
Fa0/3 notconnect 1 auto auto 10/100BaseTX
Fa0/4 notconnect 1 auto auto 10/100BaseTX
Fa0/5 notconnect 1 auto auto 10/100BaseTX
Fa0/6 notconnect 1 auto auto 10/100BaseTX
```
**Clear MAC address**
```
// clear all dynamic MAC addresses
SW1#clear mac address-table dynamic

// Clear dynamic MAC address with a given Address
SW1#clear mac address-table dynamic address <mac-address>

// Clear dynamic MAC address associated with a given switchport interface
SW1#clear mac address-table dynamic interface <interface>
```

## Router Interfaces
```
Router#show ip interface brief

Interface IP-Address OK? Method Status Protocol

GigabitEthernet0/0 unassigned YES unset administratively down down
GigabitEthernet0/1 unassigned YES unset administratively down down
GigabitEthernet0/2 unassigned YES unset administratively down down
Vlan1 unassigned YES unset administratively down down
```
**Display Interface Configuration**
```
Router#show interfaces g0/0

GigabitEthernet0/0 is administratively down, line protocol is down (disabled)
Hardware is CN Gigabit Ethernet, address is 0060.3e72.3101 (bia 0060.3e72.3101)
MTU 1500 bytes, BW 1000000 Kbit, DLY 10 usec,
reliability 255/255, txload 1/255, rxload 1/255
Encapsulation ARPA, loopback not set
Keepalive set (10 sec)
Full-duplex, 100Mb/s, media type is RJ45
output flow-control is unsupported, input flow-control is unsupported
ARP type: ARPA, ARP Timeout 04:00:00,
Last input 00:00:08, output 00:00:05, output hang never
Last clearing of "show interface" counters never
Input queue: 0/75/0 (size/max/drops); Total output drops: 0
Queueing strategy: fifo
Output queue :0/40 (size/max)
5 minute input rate 0 bits/sec, 0 packets/sec
5 minute output rate 0 bits/sec, 0 packets/sec
0 packets input, 0 bytes, 0 no buffer
Received 0 broadcasts, 0 runts, 0 giants, 0 throttles
0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored, 0 abort
0 watchdog, 1017 multicast, 0 pause input
0 input packets with dribble condition detected
0 packets output, 0 bytes, 0 underruns
0 output errors, 0 collisions, 2 interface resets
0 unknown protocol drops
0 babbles, 0 late collision, 0 deferred
0 lost carrier, 0 no carrier
0 output buffer failures, 0 output buffers swapped out

Router#
```


```
0100.0ccc.cccd
0180.c200.0000

10 mbps 2,000,000
100 mbps 200,000
1 gb 20,000
10 gb 2,000
100 gb 200
1 tb 20

// show etherchannel load balancing options
SW#show etherchannel load-balance

// set load balancing settings
SW(config)#port-channel load-balance 

PAgP (Port Aggregation Protocol) (desiriable, auto)
LACP 802.3ad (Link Aggregation Control Protoco) (active, passive)
Static mode (on)

// assign interfaces to a group. The protocol used for the port-channel will be atuomatically picked based on the option picked (desirable, auto, active, passive).
SW(config-if)#channel-group <number> mode active

// manually specify the protocol to use for the port-channel
SW(config-if)#channel-protocol PAgP/LACP



// Configure the port-channel created
SW(config)#interface port-channel <port-channle-number>

matching speed, 
matching duplex setting,
matching switchport mode (access, trunk)
if trunk, all interfaces in the port-channel must allow the same vlans and have the same native vlan

SW#show etherchannel summary
SW#show etherchannel port-channel

in order for two routers to become ospf neighbors, they must be in the same OSP area. Furthermore, interfaces must be in the same subnet for them to be in the same area.

the ospf process must not be shutdown

the router-id must be unique.

the hello and deat-timer must match

if ip ospf authentication-key lol, ip osf authentication is enabled, it must match between communicating interfaces.

the mtu must match

the network type must also match
11 --> 1011 --> 1000 = 8

1234:5678:90AB

1234:56ff:fe78:90AB

2 --> 0010 --> 0000 ==0
1034:56ff:fe78:90AB

ipv6 address 2001:db8::/64 eui-64
```



```
FHRR

HSRP (Active, Standby)
v1: Multicast IP (224.0.0.2), MAC (0000.0c07.acXX)
v2: Multicast IP (224.0.0.102), MAC (0000.0c9f.fXXX)
X: HSRP group number

VRRP (Master, Backup)
Multicast IP (224.0.0.18) MAC (0000.5e00.01XX)

GLBP (AVG, AVF)
Multicast IP (224.0.0.102) MAC (0007.b400.XXYY)
X: GLBP group number
Y: AVF
```



```
access-list 1 permit|deny ip wildcard-mask
clock summer-time


ntp authenticate
ntp authentication-key 1 md5 <key>

ntp peer 343 key ldkjfldj
ntp server 234534 key sjfljslfrjw



ROUTER AS A DNS SERVER

ip dns server
ip host R2 ip of R2

ip name-server 

ip domain-lookup


ROUTER AS A DNS CLIENT
ip name-server
ip domain-lookup

ip domain name lol.com
R2.lol.com


ip dhcp excluded-address lower bound and upper bound
ip dhcp pool name
network address

dns-server


Emergency
Alert 
Critical
Error 
Warning
Notice
Informational 
Debugging

Sequ:timestamp: %facility-severity-MNEMONIC:description

service timestamp log
service sequence-number

logging console severity
logginc monitory severity (must use terminal monitor for each session to view logs when connecting though vty)
logging buffered size severity
logging ip-address/ logging host ip-address (log logs to an external server)
logging trap severity (set severity for logs logged to external locatoin)

specified severity and all other severities higher than the one specified will be logged.

logs are logged to the console and buffer by default

show logging to view logs logged to ram

line console 0

logging synchronous


line console 0

password dfjlsfje
login

R1(config)#username user secret secret
line console 0
login local

exec-timeout

interface vlan 20
ip address

ip defautlt-gateway 

transport input telnet/ssh


R1(config)#enable secret
R1(config)#username ccna secret lol
access-list 1 permit host 192.168.1.1 
line vty 0 15
login local
exec-timeout min sec
transport input telnet
access-class 1 in


R#show version
R#show ip ssh
R1(config)#hostname
R1(config)#ip domain name abranlezama.com
R1(config)#crypto key generate rsa modulus 2048
R1(config)#access-list 1 permit host 192.168.1.1
ip ssh version 2
line vty 0 15
login local
exec-timeout min sec
access-class 1 in
transport input ssh

telnet ip-address

ssh -l username ip-address
ssh username@ip-address

ip ftp username
ip ftp password 

copy ftp/tftp: flash:


inside/outside locaton
local/global perspective

R1(config-if)#ip nat inside 
R1(config-if)#ip nat outside

// you need to configure an access list to specify which addresses are to be translated

R1(config)#access-list 1 permit ip wildcard
R1(config)#ip nat pool polname

R1(config)#ip nat inside source list 1 pool dl overload
R#show ip nat translations
R#clear ip nat translations
R1#show ip nat statistics

SW(config-if)#switchport mode access
SW(config-if)#switchport access vlan 10
SW(config-if)#switdhport voice vlan 11

Cisco inline power (CLP) proprietary 7 watts two pairs 

PoE (type 1) 802.3af 15 watts 2 pairs
PoE+ (type 2) 802.3at 30 watts 2 pairs
UPoE (Type 3) 802.3bt 60 watts 4 pairs
UPoE+ (Type 4) 802.3bt 100 watts 4 pairs

power inline police action err-disable
	disables interface and sends syslog message
power inline police action log
	restarts the interface and seds syslog message

one way delay 150 milliseconds or less
jitter 30 milliseconds or less
drop 1 percent or less


PCP

0 bet effort
3 critical application 
4 video
5 voice

DSCP

DF (Default forwarding) - best effort. value of 0
EF (Expedited forwarding) - low delay/jitter/ (audio). value of 46
AF (Assured forwarding) set of 12 standard values
	Fouter classes 1 - 4
	Three drop presedences 1 - 3
	Formula to convert AF to DSCP = 8*class + 2*drop-presedence
	uses left most 3 bits for class and next 2 for drop precedence. right-most bit is always set to 0
CS (Class selector ) Set of 8 standard values that is compatible with IPP (IP Presedence)
	uses left most 3 bits and the next 3 bits are set to 0
	formula to convert CS value to DSCP value is 8 * CS-value (0 - 7)

AF4y - interactive video
AF3y - streaming video
AF2y high priority data
DF - best effort
EF - voice traffic

minimum 8 characters
combination of numbers and letters
upper case and lower case letters
use special symbils
change password frequently


MFA
something you know
somethign you have
something you are

CSR, CA

Radius udp 1812, udp 1813
Tacacs+ TCP 49

violation modes 

switchport port-security violation shutdown|restrict|protect

shutdown 
	puts the interface in an err-disabled state
	sends syslog and/or snmp message
	increments violation counter to 1, but will be reset to 0 when the interface is reenabled.

Restrict
	The traffic is dropped
	sends syslog and/or snmp message
	interface is not disabled
	increments violation counter
Protect
	the traffic is dropped
	does not send syslog and/or snmp message
	interface is not disabled
	does not increment violation counter.


show mac address-table secure
	
```