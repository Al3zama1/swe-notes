## What is a LAN ?
* A LAN is a single **broadcast domain**, including all devices in that broadcast domain.
* A **broadcast domain** is  the group of devices which will receive a broadcast frame (destination MAC FFF.FFFF.FFFF) sent by any one of the members.
The picture below contains 5 broadcast domain, therefore there is 5 separate LANs
![LAN broadcast domain](./img/LAN-broadcast-domain.png)

## VLAN
A VLAN is a way to logically split up a layer 2 broadcast domain to make multiple separate broadcast domains.

#### Why are VLANs Needed ?
The example below shows a single LAN with different departments where a computer in the engineering department sends a broadcast message intended for other PC's in the same department. However, since there is no clear division between the different departments in the LAN, all PC's in all departments will receive the broadcast message.
![example without VLAN](./img/no-vlan.png)
* **Performance Issues**: Lots of unnecessary broadcast traffic can reduce network performance. 
	* Above, a broadcast message was intended for the Engineering department, but was propagated to all hosts in all departments.
	* Minimize unnecessary traffic in the network.
* **Security Reasons**: Even within the same office, you want to limit who has access to what.
	* Configuring security policies on a router/firewall does not have any effect on hosts communicating in the same LAN.
	* PCs in the same LAN can reach each other directly, without passing through the router.

#### Layer 3 Segmentation
The 3 departments have been separated into 3 different subnets to provide Layer 3 separation.
![VLAN misconfiguration](./img/vlan-misconfiguration.png)
* Although the three departments have been separated into three subnets (Layer 3), they are still in the same broadcast domain (Layer 2).
* The switch has no notion of Layer 3 IP addresses, it only looks at the layer 2 address. It will look that the address is the broadcast address and consequently forward the frame to all connected hosts.
* One solution would be to use a different Switch device for each of the subnets.
	* This might not be practical because most likely not all Switch interfaces will be used per subnet. Resulting in high cost and wasted Switch interfaces.

#### Layer 2 Segmentation
The switch interfaces are configures to be in a specific VLAN to provide Layer 2 separation.
![layer 2 segmentation](./img/vlan-layer2-segmenting.png)
* The end hosts belong to the VLAN configured on the Switch interface that they are connected to.
* A switch will not forward traffic between VLANs, including **broadcast/unknown unicast*** traffic.
* The switch does not perform **inter-VALN Routing**. It must send the traffic through the router to change VLAN.
* **NOTE**: Same subnet communication between two hosts is not possible if they are connected to interfaces that are configured with different VLANs.

#### VLAN Configuration
 ![VLAN configuration](./img/vlan-configuration.png)

##### Display VLANs
```
Switch#show vlan brief

VLAN Name           Status         Ports

1    default        active         Fa0/1, Fa0/2, Fa0/3, Fa0/4
		
								   Fa0/5, Fa0/6, Fa0/7, Fa0/8
			
			                       Fa0/9, Fa0/10, Fa0/11, Fa0/12
			
								   Fa0/13, Fa0/14, Fa0/15, Fa0/16
			
								   Fa0/17, Fa0/18, Fa0/19, Fa0/20
			
								   Fa0/21, Fa0/22, Fa0/23, Fa0/24
			
								   Gig0/1, Gig0/2

1002 fddi-default   active

1003 token-ring-default active

1004 fddinet-default active

1005 trnet-default active
```
* All Switch interfaces are in VLAN 1 by default.
* VLANS 1002, 1003, 1004, 1004, 1005 are for old technologies that are not needed for the CCNA.
* VLANs 1, 1002 - 1005 exist by default and **cannot be deleted**.

##### Set VLANs
```
SW1(config)#interface range g1/0 - 3
SW1(config-if-range)switchport mode access
// creates VLAN if it doesn't aready exists
SW1(config-if-range)switchport access vlan 10
Access VLAN does not exist. Creating Vlan 10

// Manual explicit creation of a VLAN
SW1(config)#vlan 10
SW1(config-vlan)#name ENGINEERING // change default VLAN name.
```
* Use `switchport mode access` to set the interface as an access port.
	* A switch port connected to an end host should enter access mode by default. However, it's better to explicitly configure the setting and not rely on auto negotiation.
* An **access port** is a  switch port  which belongs to a single VLAN, and usually connects to end hosts like PCs.
	* Its called an access port because it gives the end hosts access to the network.
* There is another is another type of switch port called **trunk port** that can carry multiple VLANs.
