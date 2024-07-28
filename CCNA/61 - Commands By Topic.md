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

// create the VRFs
R(config)#ip vrf name
R(config-if)#ip vrf forwarding name
ip address 192.168.

#show ip vrf
#show ip route
#show ip route vrf name

ping vrf name ip




// create vrf
R(config)#ip vrf name

// assign router interface to vrf created
R(config-if)#ip vrf forwarding name
R(config-if)#ip address 192.168.1.1

// show vrf
R#show ip vrf

// show ip route
R#show ip route vrf name

// ping an address located inside of a vrf
R#ping vrf name ip



R(config)#ip vrf name
R(config-if)#ip vrf forwarding name

R#show ip vrf
R#show ip route vrf name

R#ping vrf name ip


802.11 2mbps 2.4
802.11a 54mbps 5
802.11b 11mbps 2.4
802.11g 54mbps 2.4
802.11n 600mbps 2.4/5 wifi 4
802.11ac 6.93gbps 5 wifi 5
802.11ax 4*802.11ac 2.4/5/6 wifi 6

Frame control 2
	time and subtype of frame
Duration/ID 2
	time in microseconds the chanel will be dedicated to sendinding frame
	The association between the wireless client and the AP
Address 1, 2, 3 6
Sequence control 2
	Used for reasembling and removing duplicate frames
Address 4 6
QoS control 2
HT control 4
	used to faccilitate hight throughput
packet variable size
FCS 4

Destiantion address
source address
transmitter address
receiver address
\

local
flexConnect
sniffer
monitor
rogue detector
SE-connect
bridge/mesh
Fex Plus bridge


unified wlc deploymnet
cloud-based wlc deployment
embedded wlc deployment
Cisco mobility express elc deployment

AP deployment options
Autonomous APs
Lightweight APs (Split-MAC architecture)
Cloud-based APs

Autonomous APs operational modes
repeated
WGB workgroup bridge
outdoor bridge

Lighthweight APs operational modes
local
flexConnect
sniffer
monitor
rogue detector
SE connect
Bridge/Mesh
Flex plus Bridge

WLC deployment options
Unified WLC deploymbnet 6000
Cloud-based WLC deploymnet 3000
embedded WLC deploymnet 200 
Cisco Mobility Express deploymnet 100

WPA 3 additional security features
* PMF (protected management frames)
* SAE (Simultaneous authentication of equals)
* Forward secrecy

Open Flow
Cisco OpenFlex
Cisco OpenPK
Netconf

Ternary Content Addressable Memmroy
TCAM

ASIC Application Specific Integrated Circuit

Open flow
Cisco OPenFlex
Cisco OpenPK
NETCONF

ASIC (Applicatin specific integrated circuit)
TMAC (Ternary content Addressable memmory)

DNA Center (Digital Network Architecture Center) is the controller in SD-Access which is Ciscos SDN solution.

LISP (Locator ID Separation Protocol) is the control plane that keeps mappings of EIDs (Endpoint Identifiers) to RLOCs (Routing locators).

EIDs specify to what Edge node an end host is connected to
RLOCs specify the Edge node that is needed to reach a specific end host

VXLAN (Virtula Extensible LAN) is the data plane which is used to send traffic between devices. It is located in the overlay.

Underlay is made up of devices that use layer 3 switches and rotuerd ports with IS-IS.

Ansible has control node
inventory
template
variables
playbook

it is clientless
uses YAML 
its template is done via jinja2


Puppet pupptet master
client and clientless trhough proxying
variables
manifest

resources 
recipes
cookbooks
run-list

cheff 10002
puppet 8140


(config)#ip vrf name
(config-if)#ip vrf forwarding name
show ip vrf
show ip route vrf name
ping vrf name ip

Application specific integrated circuit
ternary code-addressable memmory

absorbtion
reflection
refraction
difraction
scattering

2.400GHz - 2.4835GHz
5.150GHz - 5.825GHz

802.11 2.4 2mbps
802.11a 5 54mbps
802.11b 2.4 11mbps
801.11g 2.4 54mbps
802.11n 2.4/5 600mbps wifi 4 HT
802.11ac 5 6.93gbps wifi 5 VHT
802.11ax 2.4/5/6 802.11ac*4 wifi 6


802.11 header

frame control 2 bytes 
	contains type and subtype of frames
Duration/ID 2 bytes
	duration specifies the allotted time in microseconds to transmitting the frame
	ID is an association between the wireless client and the AP being used to transport the frame
Address1, 2, 3 (6 bytes)
Sequence control 2 bytes
	allows reordering of frames and duplicate address detection and removal
Address 4 (6 bytes)
QoS 2 bytes
	used for class of service
HTC 4 bytes
	provides high throughput capabilities
payload
	variable in size
FCS (4 bytes)
	used to detect errors in the frames

Address types
Source address: original sender
Destination address: final destination
Transmitter address: current sender of the address
Receiver address: current receiver of the address


authenticated, not associated
authenticated, associated

probe request, proble response 
	not authenticated, not associated
authentication request, authentication response
	authenicated, not associated
associated request, association response
	authenticated, associated

active scanning probe request
passive scanning beacon messages


802.11 message types
management
	used to manage the BSS
	authenitcation association

control
	control transport medium. facillitate the transportation of management and data messages
	RTS (request to send), CTS (clear to send)

data
	client traffic

autonomous APs operational modes
repeater, workgroup bridge WGB, Outdoor bridge

light weight operational modes
local (provides BSS)
FlexConnect (provides BSS)
sniffer (does not provide BSS)
monitor (does not provide BSS)
rogue detector (does not even have a raio and no BSS)
SE-Connect (analyzes channels)
Bridge/Mesh Bridge mode or mesh like in autonomous
Flex plus Bridge Bridge plus the benefits of Flex which allows locally switching traffic to wired network


Cloud based APs use an WLC that is located on the cloud (eg. Meraki). However, only management traffic is sent to the WLC. regular traffic is sent directly to the APs, wired network. trunks are used. basically the same as autonomous APs in regards to traffic flow, but with the addition of central APs managemeent


WIRELESS LAN CONTROLLERS DEPLOYMENTS

Unified WLC deployment 6000
Cloud-based WLC deployment 3000
Embedded WLC deployment 200
Cisco Mobility express 100

Wireless authentication methods

Open authentication
users are allowed to enter but once inside, it can require users to authenticate in order to obtain network access

WEP (authentication and encryption)
the client and server share a key (40 or 104 bits in length) which is combined with a 24 IV to create strong 
the server sends a chanllenge frace, client

EAP (Extensible Authentication Protocol)
	EAP integrates with 802.1x for enterprise
		suplicant
		authenticator
		authentication server
EAP-FAST (flexible authentication via secure tunneling)
the server sends a PAC (protection access credentials) to the client which is used in the next step to create a secure tunnel. authentication is carried out in the tunnel

PEAP (protected EAP)
	The authentication server sends a digital certificate which is used by the client to authenticate the server and create a secure tunnel in the next step to carry out authentication 
	authenticsation is usually carried out using MS-chap

EAP-TLs
both the client and authentication server have digital certificates to create secure tunnel. in the tunnel encryption is negotiated.


WPA3 additional security features
	PMA (protected management frames) protects management frames in 802.11
	SAE (simultaneous authentication of equals)
		protect four way handshake used in personal mode when authenticating to a wireless network
	forward secrecy
	protects agains saving of packets and trying to decrypt them in teh future


management and control plane use the cpu

the data plane relies on fast forwarding, therefore it uses a Application specific integrated circuit

for example mac addresses are saved in TCAM (ternary content-addressable memory)

// create vrf
(config)#ip vrf name

// assign vrf to router interface
(config-if)#ip vrf forwarding name

show ip vrf

show ip route vrf name

ping vrf name ip-address

2.4 is from 2.400 - 2.4835
5 is from 5.150 - 5.825

frame control
duration/ID
address 1 - 3
Sequence control
address 4
QoS Control
HTControl 
payload
FCS

source, destination, transmitter, receiver

not authenticated, not associated, 
authenticated, not associated,
authenticated, associated

light weight operational modes


local 
flexConnect
sniffer
monitor
rogue detector
SE-Connect
Bridge/Mesh
Flex plus bridge

unified, cloud-based, embedded, Cisco Mobility Express

Open authenitcation 
WEP
lightweight EAP
EAP-FAST
PEAP
EAP-TLS

WEP
TKIP
CCMP (AES, CBC-MAC)
GCMP (AES, GMAC)

PMF (protected management frames) protects management frames from eavesdropping
SAE (simultaneous authentication of equals) protects the four way handshake in personal mode

forward secrecey prevents storage of frames for future decryption

cache/noncached, uniform interface, stateless, layered system, 

Application specific integrated circuit

Ternary Content-Addressable memory

OpenFlow
cisco openFlex
Cisco onePK
netconf

uniform interface,
client-server
stateless
cacheable/noncacheable,
layered system
code on demand

Openflow
cisco openflex
cisco onePK
netconf



1 hello discovery and mainance of neighbors
DBD database descritiopn used in extart and exchange
	used in extart to decide on master and slave rotuer to decide who will begin the exchange of if




pvst mac 0100.0ccc.cccd
standard 0180.c200.0000


0
16
32
48
64

c = 12

1100



dequence:timestamp: %facility-severity-MNEMONIC:description


0 emergency
1 alert
2 critical
3 error
4 warning
5 notice
6 informational
7 debugging

facility is the process in the device that originated the error
mnemonic is a short code that describes the issue
description states detailed description of the error


sequence and timestamps are not enabled by default

service timestamps log
service sequence-numbers



hostname sdfsdf
ip domain name dfsdfsdf
crypto key generate rsa modulus

ip ssh version 2

enable secret
access-list 1 permit host ip

line vty 0 15
login local
exec-timeout min sec
transport input ssh
access-class acl in


ip dhcp snooping information option
ip dhcp snooping limit rate

errdisable recovery casue psecure-violation
errdisable recovery cause dhcp-rate-limit
errdisable recovery cause arp-inspection

show ip dhcp snooping binding


T1 - 1.544
T2 = 6.312
T3 = 44.736


E1 - 2.048
E2 - 8.448
E3 = 34.368

R#show ip vrf
R#show ip route vrf name
R#ping vrf name ip

R(config)#ip vrf name
R(config-if)#ip vrf forwarding name
```