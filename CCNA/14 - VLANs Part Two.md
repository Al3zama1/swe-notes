#### Inter-VLAN Routing Methods
* Dedicated interface for each VLAn between router and switch.
	* This works, but if you have many VLANs you probably won't have enough interfaces on the router for all VLANs.
* Router on a stick(ROAS), which uses a single trunk connection to carry traffic for all VLANs between the switch and router.
	* It's efficient in terms of interfaces because only 1 is used.
	* However, in a busy network, all of the traffic going to the router and back to the switch in a single interface can cause network congestion.
	* Therefore, in large networks, a multilayer switch is the preferred method of inter-VLAN routing.
* A multilayer Switch can also be used to perform inter-VLAN routing without the need to go to the router.
## Layer 3 (Multilayer) Switches
* A multilayer switch is capable of both switching and routing.
* It is Layer 3 aware.
* Its interfaces can be configured to behave like router interfaces and assign IP addresses to them.
* It can have **Switch Virtual Interfaces (SVI)**.
* Routes can be configured on it, just like a router.
#### Switch Virtual Interfaces (SVI)
* Switch Virtual Interfaces (SVI) can be created for each VLAN to allow for inter-VLAN communication. Each SVI is given an IP address that helps establish a link between a subnet and a VLAN.
* SVIs are set up as the default gateway for all the clients in their respective VLANs, instead of the router. This avoids sending frames to the router for inter-VLAN routing.
* When a frames arrives, it will forward it to the VLAN that is associated with the subnet where the destination IP belongs.

The example below shows the process of communication between two PCs in different VLANS when a Layer 3 switch is used.
![multilayer switch inter vlan routing](./img/multilayer-switch-inter-vlan-routing.png)
* PC in VLAN 20 sees that its target is in a different subnet, therefore it will communicate with its default gateway.
	* The default gateway for VLAN 20 is SVI with IP 192.168.1.126.
* SW2 will see that the destination IP belongs in the subnet associated with VLAN 10, therefore it will forward the frame to VLAN 10. Effectively carrying out inter-VLAN routing.
* It is assumed that SW2 already has the mac address from the destination PC in its mac address table. Otherwise, the switch would have flooded VLAN 10 to find it.
#### Communication Outside the LAN
The example below shows the process of communication between two devices that are not in the same LAN.
![Multilayer switch communication outside of LAN](./img/multilayer-switch-connect-to-internet.png)
* PC in VLAN 20 sees that its target is in a different subnet, therefore it will communicate with its default gateway.
* The switch will see that the destination IP address is not in any of the subnets associated with the SVIs. Therefore, it will communicate with its configured default route.
	* For its default route, interface G0/1 was configured as a router interface and assigned an IP address. Communication will go that way to the Router for outside the LAN communication.
#### Multilayer Switch to Router Configuration
```
R1(config)#default interface g0/0 // reset interface config
R1(config)#interface g0/0
R1(config)#ip address 192.168.1.194 255.255.255.252


SW2(config)#default interface g0/1 // reset interface config
SW2(config)#ip routing // allow the switch to build a routing table
SW2(config)#interface g0/1
SW2(config-if)#no switchport
SW2(config-if)#ip address 192.168.1.193 255.255.255.252
SW2(config-if)#exit
SW2(config)#ip route 0.0.0.0 0.0.0.0 192.168.1.194

```
* `ip routing` enables Layer 3 routing on the switch and allows the creation of a routing table.
* `no switchport`
	* Configures the interface as a Layer 3 port, not a Layer 2 switchport.
#### Switch Virtual Interface Configuration
```
SW2(config)#interface vlan 10
SW2(config-if)#ip address 192.168.1.62 255.255.255.192
SW2(config-if)#no shutdown

SW2(config)#interface vlan 20
SW2(config-if)#ip address 192.168.1.126 255.255.255.192
SW2(config-if)#no shutdown

SW2(config)#interface vlan 30
SW2(config-if)#ip address 192.168.1.190 255.255.255.192
SW2(config-if)#no shutdown
```
* SVIs are shutdown by default, so remember to use `no shutdown`.
### Requirements for a SVI to be `up/up`
* The VLAN for which the SVI is being created must exist on the switch.
	* Creating a SVI for a non-existing VLAN, will not create the VLAN automatically.
	* The SVI will appear with a status and protocol set to down.
* The switch must have at least one access port in the VLAN in an up/up state, and/or one trunk port that allows the VLAN that is in an u/up state.
* The VLAN must not be shutdown (you can use the `shutdown` command to disable a VLAN).
* The SVI must not be shutdown (SVIs are disabled by default).