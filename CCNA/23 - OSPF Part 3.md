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
* In the broadcast network type, routers only form a full OSPF adjacency with the DR and BDR of the segment/subnet.
	* Therefore, routers only exchange LSAs with the DR and BDR. DROthers will not exchange LSAs with each other.
	* All routers will still have the same LSDB, but this reduces the amount of LSAs flooding the network.
#### Broadcast DR/BDR Election
* The DR/BDR election order of priority:
	1. Router with the highest **OSPF interface priority**
		* The default OSPF interface priority is 1 on all interfaces. Therefore, the Router ID will be the deciding factor.
	2. Router with the highest OSPF Router ID
* First place becomes the DR for the subnet, second place becomes the BDR.

Following the election process, R5 becomes the DR and R4 the BDR for the subnet `192.168.2.0/29`
![DR/BDR election](./img2/dr-bdr-1.png)
##### Set OSPF Interface Priority
* If you set the OSPF interface priority to 0, the router cannot be the DR/BDR for the subnet no matter what.
* The DR/BDR  election process is 'non-preemptive'. Once the DR/BDR are elected they will keep their role until OSPF is reset, the interface fails/is shutdown, etc.
	* It's a bad idea to reset OSPF in a live network.

R2's G0/0 interface priority is increased to make it the DR.
```
R2(config)#interface g0/0
R2(config-if)#ip ospf priority ?
	<0-255>
R2(config-if)#ip ospf priority 255
```
![DR/BDR election](./img2/dr-bdr-2.png)
* R4 became the DR, not R2. R2 became the BDR.
	* When the DR goes down, the BDR becomes the new DR even if it doesn't have the highest OSPF interface priority / RID . Then an election is held for the next BDR.
* DROthers (R3 and R5 in the subnet) will only move to the Full state with the DR and BDR. The neighbor state with other DROthers will be 2-way.
	* DROthers don't form full adjacencies with other DROthers. They remain in the 2-way state.


##### Reset OSPF Process
`R5#clear ip ospf process`

### OSPF Point-to-Point Network Type

## OSPF Neighbor/Adjacency Requirements

## OSPF LSA Types

