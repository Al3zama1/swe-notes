## Intro to WANs
* WAN stands for Wide Area Network.
* A WAN is a network that extends over a large geographical area.
* WANs are used to connect geographically separate LANs.
* Although the internet itself can be considered a WAN, the term WAN is typically used to refer to an enterprise's private connections that connect their offices, data centers, and other sites together.
* Over public/shared networks like the Internet, VPNs (Virtual Private Networks) can be used to create private WAN connections.
* There have been many different WAN technologies over the years. Depending on the location, some will be available and some will not be.
* Technologies which are considered 'legacy' (old) in one country might still be used in other countries.
### WAN Over Dedicated Connections (Leased Lines)
![WAN Hub-and-Spoke topology](./img4/wan-hub-and-spoke-topology.png)
* This kind of topology in which multiple devices connect to one central device is usually called a 'star' topology. However, when talking about WANs, a more common term is Hub-and-Spoke topology.
* One major advantage of a Hub-and-Spoke topology, as opposed to a full mesh topology, is that its easier to centrally control what traffic is allowed and what isn't.
	* For example, all traffic between offices can be sent to a firewall in the data center.
* This diagram is actually not exactly an accurate representation of leased lines.

![WAN over leaded line](./img4/WAN-ver-leaded-line.png)
* Rather than a single physical cable directly connecting each site, each site connect to a service provider, which connects the sites together.
* These connection use serial cables.
* However, these days WAN connections via Ethernet are more and more common.

### WAN Connection Via Ethernet (Fiber)
![WANs over Ethernet](./img4/WAN-via-Ethernet.png)
* Optical fiber connections allow much longer cables than the traditional copper UTP Ethernet cables, so these days WANs using Ethernet fiber optic cables are quite common.
### WAN over Shared Infrastructure (Internet VPN)
![WAN over VPN connection](./img4/WAN-over-VPN.png)
* The internet can also be used for an enterprise's WAN connections between sites. 
* VPNs are used to protect the communication between sites, which takes place over the internet (shared public network).
## Leased Lines
* A **leased line** is a dedicated physical link, typically connecting two sites.
* Leased lines use serial connections (PPP or HDLC encapsulation).
* There are various standards that provide different speeds, and different standards are available in different countries.
* Due to the higher cost, higher installation lead time, and slower speeds of leased lines, Ethernet WAN technologies are becoming more popular.
![Leased lines standards](./img4/leased-lines-standards.png)
## MPLS (Multi Protocol Label Switching)
* MPLS is a technology that runs in the service provider's network.
* Similar to the internet, service providers' MPLS networks are shared infrastructure because many customer enterprises connect to and share the same infrastructure to make WAN connections.
* However, the label switching in the name of MPLS allows VPNs to be created over the MPLS infrastructure through the use of **labels**.
* Some important terms:
	* CE router = Customer Edge router.
	* PE router = Provider Edge router.
	* P router = Provider core router.
* MPLS uses labels to forward traffic, not IP addresses.
*  When the PE routers receive frames from the CE routers, they add a label to the frame. 
	* The label is placed in between the Layer 2 Ethernet header and the Layer 3 IP header. Therefore, MPLS is sometimes called a Layer 2.5 protocol.
* The label is used to make forwarding decisions within the service provider network, not the destination IP.
	* In regular IP routing, the router checks the destination IP and compares it to its routing table to decide where to forward the packet. This is not the case in MPLS. MPLS routers use the MPLS label to decide where to forward the packet within the service provider network.
* The CE routers do not use MPLS, it is only used by the PE/P routers.
	* The CE routers do not have to run MPLS or even be able to run MPLS.
* There are a few kinds of VPNs that can be provided by MPLS.

![MPLS router topology](./img4/MPLS-router-topology.png)
### Layer 3 MPLS VPN
![Layer 3 MPLS VPN](./img4/layer-3-mpls-vpn.png)
* When using a Layer 3 MPLS VPN, the CE and PE routers peer using a dynamic routing protocol (OSPF etc.), for example, to share routing information.
	* The customer could also just write static routes, using the PE routers as the next hop.
* For example, in the diagram above Office A's CE will peer with one PE, and Office B's CE will peer with the other PE.
* Office A's CE will learn about Office B's routes via this OSPF peering, and Office B's CE will learn about Office A's routes too.
### Layer 2 MPLS VPN
![Layer 2 MPLS](./img4/layer-2-mpls.png)
* When using a Layer 2 MPLS VPN, the CE and PE routers do not form peerings.
* The service provider network is entirely transparent to the CE routers.
* In effect, it's like the two CE routers are directly connected.
	* Their WAN interfaces will be in the same subnet.
* If a routing protocol is used, the two CE routers will peer directly with each other.
	* In this case, the service provider network is still running MPLS just like before, but it's doing so in a way that it's like the entire service provider network is just a big switch connecting the two CE routers together.

![MPSL multiple connectivity technologies](./img4/MPLS-multiple-connectivity-technologies.png)
* Many different technologies can be used to connect to a service provider's MPLS network for WAN service.
* The sites shown above, are connecting to the service provider with a variety of connection types. They will all be able to communicate with each other over the service provider's MPLS infrastructure.
## Internet Connectivity
* There are countless ways for an enterprise to connect to the internet.
* For example, private WAN technologies such as leaded lines and MPLS VPNs can be used to connect to a service provider's internet infrastructure.
	* Although the leased line or MPLS VPN itself is a private network, it can be used as a means to access the public network that is the internet.
* In addition, technologies such as CATV (cable internet) and DSL (digital subscriber line) commonly used by customers (home internet access) can also be used by an enterprise.
* These days, for both enterprise and customer internet access, fiber optic Ethernet connections are growing in popularity due to the high speeds they provide over long distances.
### Digital Subscriber Line (DSL)
![Digital subscriber line network topology](./img4/digital-subscriber-line.png)
* DSL provides internet connectivity to customers over phone lines, and can share the same phone line that is already installed in most homes.
	* Very convenient for both, the service provider and the customer.
* A DSL modem (modular-demodulator) is required to convert data into a format suitable to be sent over the phone lines.
	* The modem might be a separate device, or it might be incorporated into the 'home router'.
	* This connects the network to the service provider over the phone line.
### Cable Internet (CATV)
![Cable internet network topology](./img4/cable-internet-topology.png)
* Cable internet provides Internet access via the same CATV (Cable Television) lines used for TV service.
* Like DSL, a cable modem is required to convert data into a format suitable to be sent over the CATV cables.
	* Like a DSL modem, this can be a separate device or built into the 'home router'.

### Redundant Internet Connections

## Internet VPNs