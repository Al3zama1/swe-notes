## Network Redundancy
* Redundancy is an essential part of network design.
* Modern networks are expected to run 24/7 365 days a year. Even a short downtime can be disastrous for a business.
* If one network component fails, you must ensure that other components will take over with little to no downtime.
* As much as possible, you must implement redundancy at every possible point in the network.

#### Network Without Redundancy
![Network without redundancy](./img/network-without-redundancy.png)
* If a failure occurs at the 'x' and the connection is lost, all hosts in the LAN lose connectivity to the internet.

#### Network With Redundancy
![Network with redundancy](./img/network-with-redundancy.png)
* Hosts in this network can take multiple paths to reach other hosts in the  LAN and to get to the internet (outside the LAN).
* The availability of multiple pathways creates network redundancy for when connections fail. 
* The redundancy added can lead to loops in the LAN, creating unnecessary traffic that affects the network performance.

## Broadcast Storms
The image below shows what would happen when PC1 tried to communicate with PC2 and PC1 didn't know the destination's MAC address.
![broadcast storms](./img/broadcast-storms.png)
* The Ethernet header doesn't have a TTL field. Broadcast frames will loop around switches in the network indefinitely. If enough of these looped broadcasts accumulate in the network, the network will be too congested for legitimate traffic to use the network. This is called a **broadcast storm**.
* Spanning Tree Protocol (STP) is a Layer 2 protocol that is used to prevent infinite loops in a LAN, just like Time to Live (TTL) is used to prevent loops at Layer 3.
* Network congestion isn't the only problem. Each time a frame arrives on a switchport, the switch uses the source MAC address field to learn the MAC address and update its MAC address table.When frames with the same source MAC address repeatedly arrive on different interfaces, the switch is continuously updating the interface in its MAC address table. This is known as **MAC Address Flapping**.
## Spanning Tree Protocol (STP)
* This section will cover **Classic Spanning Tree protocol** which is defined in IEEE 803.1D.
* Switches from all vendors run STP by default because it is very important to prevent Layer 2 loops.
* STP prevents Layer 2 loops by placing redundant ports in a blocking state, essentially disabling the interface. These interfaces act as backups that can enter a forwarding state if an active (currently forwarding) interface fails.
* Interfaces in a forwarding state behave normally. They send and receive all normal traffic.
* Interfaces in a blocking state only send or receive STP messages (called BPDUs = Bridge Protocol Date Units).
	* STP still uses the term 'bridge'. However, when we use the term 'bridge', we really mean 'switch'. Bridges are not in use in modern networks.


#### Spanning Tree Protocol Steps
1. One switch is selected as the root bridge. All ports on the root bridge are **designated ports** (forwarding state). 
	1. Root Bridge Selection:
		1. Lowest bridge ID
2. Each remaining switch will select one of its interfaces to be its **root port** (forwarding state). Ports across from the root port are always designated ports.
	1. Root Port Selection:
		1. Lowest Root cost.
		2. Lowest neighbor bridge ID.
		3. Lowest neighbor port ID.
3. Each remaining collision domain will select one interface to be a **designated port** (forwarding state). The other port in the collision domain will be **non-designated** (blocking)
	1. Designated Port Selection:
		1. Interface on switch with lowest root cost.
		2. Interface on switch with lowest bridge ID
#### Root Bridge Selection
##### STP BPDU (Bridge Protocol Data Unit)
* By selecting which ports are **forwarding** and which ports are **blocking**, STP creates a single path to/from each point in the network. This prevents Layer 2 loops.
* There is a set process that STP uses to determine which ports should be forwarding and which should be blocking.
* STP-enabled switches send/receive Hello BPDUs out of all interfaces. The default timer is 2 seconds (the switch will send a Hello BPDU out of every interface once every 2 seconds.)
* If a switch receives a Hello BPDU on an interface, it knows that the interface is connected to another switch (routers, PCs, etc. do not use STP, so they do not send Hello BPDUs).
![STP BPDU](./img/stp-bpdu.png)
##### Root Bridge
* The switch with the lowest bridge ID is elected as the root bridge. All ports on the root bridge are **designated ports**, which are in a forwarding state.
* When a switch is powered on, it assumes it is the root bridge. It will only give up its position if it receives a superior BPDU (lower Bridge ID).
* Once the topology has converged and all switches agree on the root bridge, only the root bridge sends BPDUs. Other switches in the network will forward these BPDUs, but will not generate their own original BPDUs.
* All other switches in the topology must have a path to reach the root bridge.
![root bridge selection](./img/stp-root-bridge.png)
* The Bridge Priority is compared first. If they tie, the MAC address is then compared to break the tie.
* SW1 is selected as the root bridge since all switches have the same bridge priority and it has the lowest MAC address.

**Old Bridge ID Format**
![Old bridge ID format](./img/old-bridge-id.png)
* The Bridge Priority is compared first. If they tie, the MAC address is then compared to break the tie.`
* The default bridge priority is 32768 on all switches, so by default the MAC address is used as the tie-breaker (lowest MAC address value becomes the root bridge).

**New Bridge ID Format**
![Updated bridge id](./img/updated-bridge-id.png)
* VLAN ID is included in Bridge priority because Cisco switches use a version of STP called **PVST** (Per-VLAN Spanning Tree). PVST runs a separate STP instance in each VLAN. Therefore, in each VLAN different interfaces can be forwarding/blocking.
![bridge priority structure](./img/bridge-priority.png)
* The default bridge priority used to be 32768 because it is a 16 bit field and the most significant bit is set to 1 by default.
* With the addition of the Extended System ID (VLAN ID), which sets the default VLAN to 1, the default bridge priority became 32769.
	* In the default VLAN of 1, the default bridge priority is actually 32769 (32768 + 1).
* The **bridge priority** + **extended system ID** is a single field in the Bridge ID. However, the extended system ID is set and cannot be changed because it is determined by the VLAN ID. Therefore, it is only possible to change the total Bridge Priority (Bridge Priority + Extended System ID) in units of 4096 - the value of the least significant bit of the Bridge Priority section.
* Whatever value is chosen for the Bridge Priority section will be added to the Extended System ID section to get the total Bridge Priority number.
![rood bridge with updated bridge id](./img/updated-topology-for-root-bridge.png)
* Different switches can be the root bridge in different VLANs. For example, SW1 could be the root bridge for VLAN 1, SW3 the root bridge for VLAN 2, etc...
##### Root Port Selection
* Each remaining switch will select one of its interfaces to be its **root port**. The interface with the lowest root cost will be the root port. Root ports are also in a forwarding state.
* **Root Cost**: The total cost of the outgoing interfaces along the path to the root bridge. The cost of the receiving interface is not counted.
	* When a switch has multiple interfaces with the same root cost, the interface connected to the neighbor with the lowest Bridge ID will be selected as the root port.
	* What if two switches have two connections between them and the root cost and Bridge ID are the same ? The interface connected to the interface on the neighbor switch with the lowest **STP Port ID** will become the root port. The neighbor switch's port ID is used to break the tie, no the local switch's ID.
* The ports connected to another switch's root port must be designated because the root port is the switch's path to the root bridge and other switches must not block it.

**Switch Interfaces STP Cost**
![switch interface root cost](./img/stp-root-cost.png)

![root port selection sample](./img/root-port-selection-example.png)
* SW 2:
	* Designated as the root bridge because it has the lowest Bridge Priority.
	* All its interfaces are set to designated (forwarding).
* W 1: 
	* Interface G0/0 is the root port because its root cost for the outgoing interface to get to SW2 is 4.
	* Interface G0/1 is designated because it is connected to SW3's root port.
* SW 4:
	* Interface G0/1 is the root port because its root cost for the outgoing interface to get to SW2 is 4.
* SW 3:
	* There is a tie on both interfaces for the outgoing cost to get to the root bridge.
	* SW1 has a lower Bridge ID than SW 4, therefore interface G0/0 is picked as the root bridge because you can get to SW 1 through it.

**STP Port ID**
![stp port ID](./img/stp-port-number.png)
* The port number is used as the tiebreaker if the priorities tie.
* Usually you just need to look at the port number. For example, G0/0 is lower than G1/0, etc...

Example below shows example where there is a tie for both root cost and Bridge ID. Therefore, the Interface ID is used to break the tie as explained above.
![](./img/multiple-connections-between-switches-root-port-tie.png)

##### Block Redundant Ports
![](./img/stp-block-redundant-ports.png)
* The connection between SW2 through interface G0/0 and SW3 through interface G0/1 is redundant. Therefore it must be blocked.
* However, the interfaces at both ends cannot be blocked because every collision domain must have a single STP designated port. The rules for which port is blocked are shown in the picture above.
	* When switches are used, each link is a separate collision domain. They are shown in the picture with the colored rectangles.

