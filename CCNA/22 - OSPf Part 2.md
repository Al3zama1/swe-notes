## OSPF Metric (Cost)
* OSPF's metric is called **cost**.
* It is automatically calculated based on the bandwidth (speed) of the interface.
* The formula to calculate OSPF cost is **reference bandwidth** / **interface bandwidth**.
* The default reference bandwidth is 100 mbps:
	* Reference: 100 mbps / Interface: 10 mbps = cost of 10.
	* Reference: 100 mbps / Interface 100 mbps = cost of 1.
	* Reference: 100 mbps / Interface 1000 mbps = cost of 1.
	* Reference: 100 mbps / Interface 10000 mbps = cost of 1.
* All values less than 1 will be converted to 1. Therefore, Fast Ethernet, Gigabit Ethernet, 10Gig Ethernet, etc. are equal and all have a cost of 1 by default.
* You can and should change the reference bandwidth:
	* `R1(config-router)#auto-cost reference-bandwidth <megabit-per-second>`
	* You should configure a reference bandwidth greater than the fastest link in your network(to allow for future upgrades).
	* You should configure the same reference bandwidth on all OSPF routers in the network to provide a consistent cost for each interface.
* A manually configured cost for an interface takes precedence over the auto-generated cost.
	* `R1(config-if)#ip ospf cost <cost>`
* It is recommended that you change the reference bandwidth or manually configure an interface's cost to change the OSPF cost of individual interfaces if you want.
* One more option to change the OSPF cost of an interface is to change the bandwidth of the interface with the `bandwidth` command. However, because the bandwidth value is used in other calculations, it is not recommended to change this value to alter the interface's OSPF cost.
	* `R1(config-if)#bandwidth <kilobits-per-second>`
	* Although the bandwidth matches the interface speed by default, changing the interface bandwidth doesn't actually change the speed at which the interface operates.
	* The bandwidth is just a value that is used to calculate OSPF cost, EIGRP metric, etc.
	* The command `speed` is used to change the speed at which the interface operates.
* Loopback interfaces have a cost of 1.
	* Once you are at the router, to get to one of its loopback addresses, you just add 1 to the cost.
* The OSPF cost to a destination is the total cost of the 'outgoing/exit' interfaces.

**Show OSPF Cost Associated With Interfaces**
`R1# show ip ospf interface brief`
## Becoming OSPF Neighbors
* Making sure that routers successfully become OSPF neighbors is the main task in configuring and troubleshooting OSPF.
* Once routers become neighbors, they automatically do the work of sharing network information, calculating routes, etc.
* When OSPF is activated on an interface, the router starts sending OSPF **hello** messages out of the interface at regular intervals (determined by the **hello timer**). These are used to introduce the router to potential OSPF neighbors.
	* By exchanging 'hello' messages, routers can check that they are compatible to become OSPF neighbors.
* The default hello timer is 10 seconds for an Ethernet connection.
* Hello messages are multicast to `224.0.0.5` (multicast address for all OSPF routers).
* OSPF messages are encapsulated in an IP header with a value of 89 in the protocol field.

### OSPF Message Types
![OSPF message types](./img2/OSPF-message-types.png)
### OSPF States
#### Down State
It's assumed that OSPF has just been activated on R1's G0/0 interface
![OSPF down state](./img2/OSPF-down-state.png)
* R1's G0/0 interface has just been activated as an OSPF interface, therefore it will send an OSPF *hello* message to `224.0.0.5` (multicast address for all OSPF routers).
* Two  pieces of information included in the *hello* message are:
	* The Router-ID of the router (R1) originating the *hello* message.
	* The neighbor's (R2) Router-ID, which will be set to 0.0.0.0 at this point because R1 doesn't know it yet.
* R1 doesn't know about any OSPF neighbors yet, so the current neighbor state is **down**.
#### Init
![OSPF Init State](./img2/OSPF-init-state.png)
* When R2 receives the *hello* packet, it will add an entry for R1 to its OSPF neighbor table.
	* R1 still doesn't know about the neighbor (R2), so it will not have an entry for it in its OSPF neighbor table.
* In R2's neighbor table, the relationship with R1 is now in the **init** state.
	* In the **init** state, the *hello* packet was received, but the receiving router's own Router-ID is not in the *hello* packet, as shown in the picture above.
#### 2-way
![OSPF 2-way state](./img2/OSPF-2-way-state.png)
* R2 will send a reply *hello* packet containing the RID of both routers.
* R1 will insert R2 into its OSPF neighbor table upon arrival of the reply.
* R1 will send another *hello* message, this time containing R2's RID.
* Now both routers should be in the **2-way** state.
	* The 2-way state is when a router has received a *hello* packet with its own RID in it.
	* If both routers reach the 2-way state, it means that all of the conditions have been met for them to become OSPF neighbors. They are now ready to share LSAs to build a common LSDB.
	* In some network types, a DR (Designated Router) and BDR (Backup Designated Router) will be elected at this point.
#### Exstart
* The two routers will now prepare to exchange information about their LSDB.
#### Exchange
#### Loading
#### Full

## More OSPF Configuration
