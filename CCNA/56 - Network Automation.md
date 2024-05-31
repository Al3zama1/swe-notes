## Network Automation
* Previous version of the CCNA focused on the traditional model of managing/controlling networks.
* The current version focuses on the traditional models as well, but CCNA candidates are expected to have a basic understanding of various topics related to network automation.
* In the traditional manual configuration model, engineers manage devices one at a time by connecting to their CLI via SSH.
	* Typos and other small mistakes are common.
	* It is time-consuming and very inefficient in large-scale networks.
	* It is difficult to ensure that all devices adhere to the organization's configurations.
* Network automation provides many key benefits:
	* Human error (typos etc.) is reduced.
	* Networks become much more scalable. New deployments, network-wide changes, and troubleshooting can be implemented in a fraction of the time.
	* Network-wide policy compliance can be assured (standard configuration, software versions, etc).
	* The improved efficiency of network operations reduces the opex (operating expenses) of the network. Each task requires fewer man-hours.
* There are many tools/methods that can be used to automate tasks in the network:
	* SDN (Software-Defined Networking).
	* Ansible.
	* Puppet.
	* Python scripts.
	* etc...
## Logical 'Planes' of Network Functions
* The various functions  of network devices can be logically divided up (categorized) into planes:
	* Data plane
	* Control plane
	* Management plane
* The Data plane is the reason we buy routers and switches (and network infrastructure in general), to forward messages. However, the Control plane and Management plane are both necessary to enable the data plane to do its job. 
### Data Plane
* All tasks involved in forwarding user data/traffic from one interface to another are part of the **data plane**.
* A router receives a message, looks for the most specific matching route in the routing table, and forwards it out of the appropriate interface to the next hop. It also de-encapsulates the original Layer 2 header, and re-encapsulates with a new header destined for the next hop's MAC address.
* A switch receives a message, looks at the destination MAC address, and forwards it out of the appropriate interface (or floods it). This includes functions like adding or removing 802.1q VLAN tags.
* NAT (changing the src/dst addresses before forwarding ) is part of the data plane.
* Deciding to forward or discard messages due to ACLs, port security, etc, is part of the data plane.
* The data plane is also called the forwarding plane because that is what it does, it forwards messages.
### Control Plane
* How does a device's data plane make its forwarding decisions ?
	* Devices use things like their routing table, MAC address table, ARP table, STP, among other things, to make these forwarding decisions.
* Functions that build these tables (and other functions that influence the data plane) are part of the **control plane**.
* The control plane *controls* what the data plane does, for example by building a router's routing table.
* The control plane performs overhead work.
	* OSPF itself doesn't forward user data packets, but it informs the data plane about how packets should be forwarded.
	* STP itself isn't directly involved in the process of forwarding frames, but it informs the data plane about which interfaces should and should't be used to forward frames.
	* ARP messages aren't user data, but they are used to build an ARP table which is used in the process of forwarding data.
* In traditional networking, the data plane and control plane are both distributed. Each device has its own data plane and its own control plane. The planes are distributed throughout the network.
### Management Plane
* Like the control plane, the **management plane** performs overhead work. However, the management plane doesn't directly affect the forwarding of messages in the data plane.
* The management plane consists of protocols that are used to manage devices.
	* SSH/Telnet, used to connect to the CLI of a device to configure/manage it.
	* Syslog, used to keep logs of events that occur on the device.
	* SNMP, used to monitor the operations of the device.
	* NTP, used to maintain accurate time on the device.
### Data Plane Message Forwarding Optimizations
* The operations of the Management plane and Control plane are usually managed by the CPU. 
* However, this is not desirable for data plane operations because CPU processing is slow (relatively speaking).
* Instead, a specialized hardware ASIC (Application-Specific Integrated Circuit) is used. ASICs are chips built for specific purposes (such as forwarding frames in a switch).
* Using a switch as an example:
	* When a frame is received, the ASIC (not the CPU) is responsible for the switching logic.
	* The MAC address table is stored in a kind of memory called TCAM (Ternary Content-Addressable memory).
		* Another common name for the MAC address table is CAM table.
	* The ASIC feeds the destination MAC address of the frame into the TCAM, which returns the matching MAC address table entry.
	* The frame is then forwarded out of the appropriate interface.
* Modern routers also use a similar hardware data plane: an ASIC designed for forwarding logic, and tables stored in TCAm.
* In summary:
	* When a device receives control/management traffic (destined for itself), it will be processed in the CPU.
	* When a device receives data traffic which should pass through the device, it is processed by the ASIC for maximum speed.
## Software-Defined Networking (SDN)
## APIs
## Data Serialization
