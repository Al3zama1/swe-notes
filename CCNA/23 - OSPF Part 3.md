## Loopback Interfaces
* A loopback interface is a virtual interface in the router.
* It is always up/up (unless you manually shutdown).
* It is not dependent on a physical interface. 
* It provides a consistent IP address that can be used to reach/identify the router.

## OSPF Network Types
* The OSPF 'network type' refers to the type of connection between OSPF neighbors (Ethernet, etc...).
* There are three main OSPF network types:
	* **Broadcast**: enabled by default on **Ethernet** and **FDDI** (Fiber Distributed Data Interfaces) interfaces.
	* **Point-to-point**: enabled by default on **PPP** (Point-to-point Protocol) and **HDLC** (High-Level Data Link Control) interfaces.
	* **Non-broadcast**: enabled by default on **Frame Relay** and **x.25** interfaces.
### OSPF Broadcast Network Type
* Enabled on **Ethernet** and **FDDI** interfaces by default.
* Routers dynamically discover neighbors by sending/listening for OSPF *Hello* messages using multicast address `224.0.0.5`.
* A **DR** (designated router) and **BDR** (backup designated router) must be elected on each subnet (only DR if there are no OSPF neighbors, ie. R1's G1/0 interface).
* Routers which aren't the DR or BDR become a **DROther**.
#### Broadcast DR/BDR Election
* The DR/BDR election order of priority:
* 

### OSPF Point-to-Point Network Type

## OSPF Neighbor/Adjacency Requirements

## OSPF LSA Types

