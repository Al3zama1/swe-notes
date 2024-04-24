## Why is EtherChannel Needed?
* ***Access Layer Switch**: A switch that end hots connect to.
* ***Distribution Layer Switch**: A switch that access layer switches connect to.
* ***Oversubscription**: The bandwidth of the interfaces connected to end hosts is greater than the bandwidth of the connection to the distribution switch(es). Some oversubscription is acceptable, but too much will cause congestion.

![](./img2/asw-to-dsw-with-multiple-links.png)
Let's say there are many end hosts connected to an access switch(ASW1) and they are all trying to access the internet to do their work. The network administrator notices that the connection to the distribution switch(DSW1) is congested, so he decides to add another link to increase the bandwidth and be able to support all the end hosts. The total bandwidth of the connections to the end hosts is still greater than the bandwidth of the connection to DSW1, but that's okay because not all hosts in the network are always in a constant state of sending and receiving internet traffic. However, despite the addition of multiple links between ASW1 and DSW1, the connection between the two switches is just as congested as it was with a single link.

* If you connect two switches together with multiple links, all except one will be disabled by Spanning Tree to prevent Layer 2 loops that can lead to broadcast storms.
* Other links will be unused unless the active link fails. In that case, on of the inactive links will start forwarding.

## EtherChannel
* ***EtherChannel** allows you to group multiple physical interfaces into a group which operates as a single logical interface.
* STP will treat this group as a single interface, therefore none of theme will be disabled.
* Traffic in the EtherChannel will be load balanced among the physical interfaces in the group. As a result, the bandwidth of all the interfaces in the EtherChannel can be taken advantage. It's as if the interfaces in the EtherChannel combine to form a faster virtual interface.

![EtherChannel with broadcast frame](./img2/etherchanel-with-broadcast-frame.png)
As shown above, when a PC sends a broadcast frame, ASW1 will send it out all interfaces except the one where it came in. However, the 4 links between ASW1 and DSW1 form a single virtual interface, therefore one instead of 4 frames are sent to DSW1. DSW1 also sees all four interfaces as a single virtual interface through which it received the broadcast frame, therefore it cannot send the frame back to ASW1. It can only send it out its interfaces on the right.

## EtherChannel Load-Balancing
* EtherChannel perform load balancing by using different physical interfaces in the EtherChannel for different flows.
* A flow is a communication between two nodes in the network.
* Frames in the same flow will be forwarded using the same physical interface. If frames in the same flow were forwarded using different physical interfaces, some frames may arrive at the destination out of order, which can cause problems.
	* Some applications can deal with frames arriving out of order, but some can't.
* It is possible to change the inputs used in the interface selection calculation.
* Inputs that can be used include:
	* Source MAC: All frames with the same source MAC address will always use the same interface in the EtherChannel.
	* Destination MAC: All frames with the same destination MAC address will always use the same interface in the EtherChannel.
	* Source & Destination MAC
	* Source IP
	* Destination IP
	* Source and Destination IP
* The load balance options available depend on the switch model being used.
### Show EtherChannel Configuration
```
Switch#show etherchannel load-balance
EtherChannel Load-Balancing Configuration:
src-mac

EtherChannel Load-Balancing Addresses Used Per-Protocol:
Non-IP: Source MAC address
IPv4: Source MAC address
IPv6: Source MAC address
```
### Configure EtherChannel Load Balance Options
```
Switch(config)#port-channel load-balance ?
dst-ip Dst IP Addr
dst-mac Dst Mac Addr
src-dst-ip Src XOR Dst IP Addr
src-dst-mac Src XOR Dst Mac Addr
src-ip Src IP Addr
src-mac Src Mac Addr
```

## EtherChannel Configuration Methods
* There are 3 methods of EtherChannel configuration on Cisco Switches.
	* PAgP (Port Aggregation Protocol)
		* Cisco proprietary protocol
		* Dynamically negotiates the creation/maintenance of the EtherChannel (like DTP does for trunks).
	* LACP (Link Aggregation Control Protocol)
		* Industry standard protocol (IEEE 802.3ad)
		* Dynamically negotiates the creation/maintenance of the EtherChannel (like DTP does for trunks).
		* It can be used to form EtherChannels with switches from other vendors. Because of this, LACP is the preferred method of configuring EtherChannels.
	* Static EtherChannel
		* A protocol isn't used to determine if an EtherChannel should be formed.
		* Interfaces are statically configured to form an EtherChannel.
		* This is usually avoided because you want the switches to dynamically maintain the EtherChannel.
			* For example, you want the switch to remove an interface from the EtherChannel if there is a problem with it.
* Up to 8 interfaces can be formed into a single EtherChannel (LACP allows up to 16, but only 8 will be active. The other 8 will be on standby mode, waiting for an active interface to fail).

### PAgP Configuration
```
Switch(config-if-range)#channel-group 1 mode ?
active    Enable LACP unconditionally
auto      Enable PAgP only if a PAgP device is detected
desirable Enable PAgP unconditionally
on Enable Etherchannel only
passive   Enable LACP only if a LACP device is detected

Switch(config-if-range)#channel-group 1 mode desirable
Switch(config-if-range)#
Creating a port-channel interface Port-channel 1
```