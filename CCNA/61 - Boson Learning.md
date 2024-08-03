## IP Phones Trust
The command moves the trust boundary from the switch to the IP phone, which lets the switch accept the IP phone voice traffic as having come from a trusted source.
```
mls qos trust cost
```

The switch instructs the IP phone connected to the interface to trust the CoS priority of incoming data packets. The IP phone will not override the CoS values from the host and will accept the existing CoS values as valid and forward unchanged data packets to the switch.
```
SW(config-if)switchport priority extend trust
```

The switch instructs the IP phone to reclassify the CoS priority value that the host assigns to its data packets. It will override the CoS priority value assigned by the host and tags the data packets with a CoS of 0.

Overriding the CoS priority value ensures that voice packets will have a higher priority than the data packets. Therefore, voice packets will be given preference over the data packets as they are processed by the switch.
```
SW(config-if)switchport priority extend cos
```

## 802.11 Standards
### 802.11k
Provides assisted roaming in a wireless network. A roaming wireless client can request a list of known neighboring APs that might be potential candidates for transition. The list returned by an AP is optimized for the client and contains only APs in the same wireless band with which the client is associated. This enables the client to find a new AP without needing to probe unnecessary wireless channels, which speeds transition and increases battery life for portable devices.

### 802.11r 
Provides support for fast transition (FT) roaming. A wireless client and an AP perform the Pairwise Master Key (PMK) calculation in advance. These recalculated PMK keys are then used after the client sends its re-association request to the new AP and the AP responds with its association response. It enables the client to transition to a new AP without needing to re-authenticate, thereby  speeding the handover between APs and minimizing adverse QoS effects caused by roaming.

### 802.11w
Provides management frame protection (MFP). MFP is a security mechanism that prevents management frames from being compromised by a malicious user.

### 802.11v
Provides network-assisted power saving. A wireless client can remain in a standby or sleep state longer to improve battery life. 802.11v provides a Directed Multicast Service (DMS), which enables a client to request that certain multicast messages be delivered as unicast messages instead. This enables the client to ignore the multicast messages during sleep and to receive the unicast messages at a greater rate of speed once it is active again. It also provides clients the ability to extend the amount of time they may remain idle before being disassociated with an AP.

## Access/Configure WLC Though HTTPS

Configure a WLC to support HTTPS management connections. This is allowed by default, so it must only be used if it has been previously disabled.
```
config network secureweb enable
```


## Device Password

Enter a plain text password that should be converted to an MD5 hash and stored.
```
username boson secret eX$1mM@x
```

If you already now the hash value of the password, you can use the MD5 hash value of a password manually instead of assigning a plain-text password to be converted into a hash by the IOS.
* The `5` parameter indicates that the assigned value is already in MD5 hash form.
```
username boson secret 5 eX$1mM@x
```

## Multicast MAC Address
The Ethernet multicast range of 0100:5E00:0000 - 0100:5E7F:FFFF has been allocated for IP multicast use. This means that the first 24 bitts of a 48-bit multicast MAC address are always 0100:5E, and the twenty-fifth bit is always set to 0. The remaining 23 bits are created from the last 23 bits of the multicast IP address.
* The right most bit is indicates whether the MAC address is unicast or multicast.
	* 0 - unicast
	* 1 - multicast
* The second right most bit indicates whether the address was globally or locally assigned.
	* 0 - Globally administered (OUI).
	* 1 - Locally administered.

## Late Collisions
Late collisions can be caused by a duplex mismatch and long cable segments.
* The half-duplex port that is connected to a full-duplex port can report late collisions.
* The full-duplex side will report  different errors, such as runts, FCS errors, and alignment errors.

## Protocol Numbers
* EIGRP - 88
* ICMPv6 - 58
* GRE - 47
* OSPF - 89
* ESP (Encapsulating Security Payload) - 50

## Cisco SDA & Cisco Enterprise Platforms
* **Cisco Prime Infrastructure (PI)** is the enterprise management platform that does not support Cisco SDA. Cisco PI is a traditional enterprise Cisco management platform that relies on a browser-based graphical user interface. to enable administrators to perform operations on the network, diagnose problems with the network, and interact with devices on the network.
* **Cisco DNA Center** is the enterprise management platform that is specifically built to support Cisco SDA. It abstracts the complexity of networks configuration by implementing a centralized controller and GUI. Additionally, it supports many of the same traditional campus device management features that are supported by other Cisco management solutions.
* **Cisco Network Assistant** is a LAN management platform, not an enterprise management platform. It is a free Java-based desktop application that enables a LAN administrator to perform network operations, diagnose problems, and interact with network devices by using a GUI. A typical Cisco Network Assistant installation supports the management of up to 80 devices. Furthermore, it predates Cisco SDA and does not support it.
* **Cisco IOS 15** is a network device operating system (OS), not an enterprise management platform, that is used to directly configure, manage, and troubleshoot a single device. Administrators typically interact with Cisco IOS by using a command-line interface.

## FlexConnect ACLs
FlexConnect ACLs are configured on Cisco wireless lightweight APs VLAN interfaces if the lightweight AP is operating in FlexConnect mode. One possible application of it is to prevent administration of the wireless local area network (WLAN) from a particular VLAN.
* They support the implicit deny rule.
* They are applied per AP and per VLAN.
* They are supported on the native VLAN.
* They cannot be configured with a per-rule direction.

## Split-MAC deployment Device Responsibilities
In a Cisco Unified Wireless Network deployment, the MAC functions that are normally handled by a single device in a autonomous wireless network are distributed between lightweight APs and WLCs.
* The functionality provided by the lightweight AP includes handling real-time processing of data, such as sending and receiving 802.11 traffic, responding to beacons and probe messages, encryption, and packet prioritization. In addition, the lightweight AP must send management information to the WLC so that the WLC can forward the information to a management station.
* The CLC handles tasks that are not time-sensitive, such as security management, lightweight AP configuration management, and client load balancing. The WLC is also responsible for client association requests, key exchange, security policy enforcement, and radio frequency  (RF) management.
## Cisco WLC AAA Override Feature
It can be used to configure VLAN tagging, QoS, and ACLs to individual clients based on Remote Authentication Authentication Dial-In User Service (RADIUS) attributes.

## EIGRP Tables
* The routing table contains only successor routes.
* The topology table contains only successor routes and feasible successor routes.
* The neighbors table contains routes that are not chosen as successor or feasible successor routes.
## HSRP States
* **Init**: A router enters the init state after it experiences a configuration change or when an interface becomes available. From the init state the router progresses to the learn state.
* **Learn**: The router determines the virtual IP (VIP) of the gateway and waits for hello messages from the active router. Once the router has learned the VIP, it progresses to the listen state.
* **Listen**: The router listens for hello packets from the active and standby router.
* **Speak**: A router will only enter the speak state if a router with a higher priority becomes the active router. Once the preempted router determines its standing in the router group, it will transition to either the listen state or the standby state.
* **Standby**: A standby router will assume the active state if it does not receive any hello packets from the active router for the duration of the holdtime timer, which, by default, is 10 seconds or 3 times the hello timer. After the standby router assumes the active state, the router with the next highest priority in the listen state assumes the role of the standby router.
* **Active**: The active router is used as the gateway for the network. All traffic entering and leaving the network is routed through the active router. Typically, there is only one router in the standby state and one router in the active state.

## Common Attacks
* In a **MAC flood attack**, an attacker generates thousands of forged frames every minute with the intention of overwhelming the switch's MAC address table. Once this table is flooded, the switch can no longer make intelligent forwarding decisions and all traffic is flooded. This allows the attacker to view all dat sent through the switch because all traffic will be sent out each port. Port security can help mitigate MAC flooding attacks by limiting the number of MAC addresses that can be learned on each interface to a maximum of 128. It is also knows as CAM table overflow attack.
* In a **Spoofing attack**, an attacker uses the MAC address of another known host on the network in order to bypass port security measures. MAC spoofing can also be used to impersonate another host on the network. Implementing port security with sticky secure MAC addresses can help mitigate MAC spoofing attacks.
* In a **ARP poisoning attack** also known as ARP spoofing, the attacker sends GARP messages to hosts. The GARP messages associate the attacker's MAC address with the internet protocol address of a valid host on the network. Subsequent traffic sent to the valid host address will go through the attacker's computer rather than directly to the intended recipient. Implementing Dynamic ARP Inspection (DAI) can help mitigate ARP poisoning attacks.
* In a **VLAN hopping attack**, an attacker attempts to inject packets into other VLANs by accessing the VLAN trunk and double-tagging 802.1Q frames. A successful VLAN hopping attack enables an attacker to send traffic to other VLANs without the use of a router. VLAN hopping can be prevented by disabling DTP on trunk ports, changing the native VLAN, and by configuring user-facing ports as access ports.
* In a **DHCP spoofing attack**, an attacker installs a rogue DHCP server on the network in an attempt to intercept DHCP requests. The rogue DHCP server can then respond to the DHCP requests with its own IP address as the default gateway address; hence all traffic is routed through the rogue DHCP server. DHCP snooping can be used to prevent DHCP spoofing attacks.

## Cisco Application Centric Infrastructure (ACI)
The ACI infrastructure implements the Spine-Leaf architecture. Each leaf node must connect to every spine node and each spine node must connect to every leaf none. Cisco ACI is a data center technology that uses switches, categorized as spine and leaf nodes, to dynamically implement network application policies in response to application-level requirements. Network application policies are defined on a Cisco Application Policy Infrastructure Controller (APIC) and are implemented by the spine and leaf nodes.

The spine leaf nodes create a scalable network fabric that is optimized for east-west data transfers, which in a data center is typically traffic between an application server and its supporting data services, such as database or file servers. Despite its lack of fully meshed connections between spine nodes or between leaf nodes, this physical topology enables nonlocal traffic to pass from any ingress leaf interface to any egress leaf interface though a single, dynamically selected spine node. The spine node is dynamically/randomly selected to achieve load balancing and not overburden spine nodes. By contrast, local traffic is passed directly from an ingress interface on the leaf node to the appropriate egress interface on the same leaf node.

Because a spine node has a connection to every leaf node, the scalability of the fabric is limited by the number of ports on the spine node, not by the number of ports on the leaf node. If additional access ports are needed, a new leaf node can be added to the infrastructure as long as there is sufficient number of ports remaining on the existing spine nodes to support the new lead node.

Redundant connections between the spine and leaf pair are unnecessary because the nature of the topology ensures that each leaf has multiple connections to the network fabric. Therefore, each spine node requires only a single connection to each leaf node. Redundancy is also provided by the presence of multiple APICs, which are typically deployed as a cluster of three controllers. APICs are not directly involved in forwarding traffic and are therefore not required to connect to every spine or leaf node. Instead, the APIC cluster is connected to one or more leaf nodes in much the same manner that other endpoint groups (EPGs), such as application servers, are connected. Because, APICs are not directly involved in forwarding traffic, the failure of an APIC does not affect the ability of the fabric to forward traffic.