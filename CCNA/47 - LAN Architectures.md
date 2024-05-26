* You have studies various networking technologies: routing, STP, EtherChannel, OSPF, FHRPs, switch security features, etc.
* There are standard 'best practices' for network design.
	* However there are a few universal 'correct answers'.
	* The answer to most general questions about network design is 'it depends'.
* In the early stages of your networking career, you probably won't be asked to design networks yourself.
* However, to understand the networks you will be configuring and troubleshooting, it's important to know some basics of network design.
## Common Terminologies
### Star Topology
![Star topology diagram](./img3/star-topology.png)
* When several devices all connect to one central device, we can draw them in a 'star' like shape. Therefore, this is often called a 'star topology'.
* Note that in network diagrams the devices might be drawn in the shape of a star. But if many devices are connected to one central device, we can call it a star topology, regardless of how the diagram is drawn.
### Full Mesh
![Full Mesh topology](./img3/full-mesh-topology.png)
* A **Full Mesh** topology is formed when each device is connected to each other device.
### Partial Mesh
![Partial Mesh topology](./img3/partial-mesh-topology.png)
* A **Partial Mesh** topology is formed when some devices are connected to each other, but not all.
## 2-Tier LAN Architecture
* The two-tier LAN design consists of two hierarchical layers:
	* **Access Layer**
	* **Distribution Layer**
* Also called a 'Collapsed Core' design because it omits a layer that is found in the Three Tier design: the **Core Layer**

### Access Layer
* The layer that end hosts connect to (PCs, printers, cameras, etc.).
* Typically Access Layer Switches have lots of ports for end hosts to connect to.
* QoS marking is typically done here because it's a good practice to mark traffic as early as possible in the network.
* Security services like port security, DAI (Dynamic ARP Inspection), etc are typically performed here.
* Switchports might be PoE-enabled for wireless Access Points, IP phones, etc.
### Distribution Layer
* Aggregates connections from the Access Layer Switches.
	* Connections from access layer switches are usually aggregated to a redundant pair of distribution layer switches.
* Typically is the border between Layer 2 and Layer 3 in the network. 
* Runs Layer 2 and Layer 3 protocols since it is concerned with both Layers.
* Connects to services such as Internet, WAN, etc.
* This is not always the case, but usually the connections from the access layer switches to the distribution layer switches are Layer 2 connections, and the end hosts use the SVIs on the distribution layer switches as their default gateways.
### 2-Tier Campus Lan Design
![2-tier campus LAN design](./img3/two-tier-campus-lan-design.png)
* The connections between distribution switches and access layer switches are Layer 2 and loops can occur.
## Spine-Leaf Architecture (Data Center)
## SOHO (Small Office/Home Office)
