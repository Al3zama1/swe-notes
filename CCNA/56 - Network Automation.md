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
* A router receives a message, looks for the most specific matching route in the routing table, and forwards it out of the appropriate interface to the next hop. It also de-encapsulates the original Layer 2 header, and re-encapsulates it with a new header destined for the next hop's MAC address.
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
* Instead, a specialized hardware **ASIC** (Application-Specific Integrated Circuit) is used. ASICs are chips built for specific purposes (such as forwarding frames in a switch).
* Using a switch as an example:
	* When a frame is received, the ASIC (not the CPU) is responsible for the switching logic.
	* The MAC address table is stored in a kind of memory called **TCAM** (Ternary Content-Addressable memory).
		* Another common name for the MAC address table is CAM table.
	* The ASIC feeds the destination MAC address of the frame into the TCAM, which returns the matching MAC address table entry.
	* The frame is then forwarded out of the appropriate interface.
* Modern routers also use a similar hardware data plane: an ASIC designed for forwarding logic, and tables stored in TCAM.

* In summary:
	* When a device receives control/management traffic (destined for itself), it will be processed in the CPU.
	* When a device receives data traffic which should pass through the device, it is processed by the ASIC for maximum speed.
## Software-Defined Networking (SDN)
* **Software-Defined Networking (SDN)** is an approach to networking that centralizes the control plane into an application called a controller.
* SND is also called **Software-Defined Architecture (SDA)** or **Controller-Based Networking**.
* In traditional networking, the data plane and control plane are both distributed. Each device has its own data plane and its own control plane. The planes are distributed throughout the network.
* A SDN controller centralizes control plane functions like calculating routes.
	* This is just an example, and how much the control plane is centralized varies greatly.
* The controller can interact programmatically with the network devices using APIs.

![Software-Defined networking architecture](SDN-SBI.png)
* The communication between the devices and the controller is done via what's called the southbound interface (SBI).
* Even though this diagram shows a totally centralized control plane, in reality there are many different solutions.
	* Some solutions centralize the entire control plane, and some of them only centralize some functions of the control plane.
### Southbound Interfaces (SBI)
* The SBI is used to communicate between the controller and the network device it controls.
	* It's called southbound because in diagrams we usually draw the controller on top and the network devices on the bottom (the south).
* The SBI is not a physical interface, it's a software interface that allows the controller and network devices to communicate.
* It typically consists of a communication protocol and API.
* APIs facilitate data exchanges between programs.
	* Data is exchanged between the controller and the network devices.
	* An API on the network devices allows the controller to access information on the devices, control their data plane tables, etc.
* Some examples of SBIs:
	* OpneFlow
	* Cisco OpenFlex
	* Cisco onePK (Open Network Environment Platform Kit)
	* NETCONF
### Northbound Interface (NBI)
![NBI diagram](SDN-NBI.png)
* Using the SBI, the controller communicates with the managed devices and gathers information about them:
	* The devices in the network
	* The topology (how the devices are connected together)
	* The available interfaces on each device
	* Their configurations
* The **Northbound Interface (NBI)** is what allows us to interact with the controller, access the data it gathers about the network, program it, and make changes in the network via the SBI.
	* It's called northbound because in diagrams we usually draw the controller in the middle and the 'App' on top (the north).
* The NBI is not a physical interface, it's a software interface that allows the controller and apps to communicate.
* A REST API is used on the controller as an interface for apps to interact with it.
	* REST = Representational State Transfer.
* Data is sent in a structured (serialized) format such as JSON, XML.
	* It makes it much easier for programs to use the data because it's stored in a standard format that is easy to interact with.
## Automation in Traditional Networks vs SDN
* Networking tasks can be automated in traditional networks:
	* Scripts can be written (ie. using python) to push commands to many devices at once.
	* Python with good use of Regular Expressions can parse through `show` commands to gather information about the network devices.
* However, the robust and centralized data collected by SDN controllers greatly facilitates these functions.
	* The controller collects information about all devices in the network.
	* Northbound APIs allow apps to access information in a format that is easy for programs to understand (ie. JSON, XML).
		* No need to write scripts to parse though specific `show` commands to get the information you want.
	* The centralized data facilitates network-wide analytics.
* SDN tools provide the benefits of automation without the requirement of third-party scripts & apps. 
	* You don't need experience in automation to make use SDN tools.
	* However, APIs allow third-party applications to interact with the controller, which can be very powerful if you're able to create your own apps.
* Although SDN and automation aren't the same thing, the SDN architecture greatly facilitates the automation of various tasks in the network via the SDN controller and APIs.