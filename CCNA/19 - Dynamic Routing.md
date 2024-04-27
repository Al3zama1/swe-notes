## Introduction to Dynamic Routing Protocols
* **Network Route***: A route to a network/subnet (mask length < /32).
* **Host Route**: A route to a specific host (/32 mask).
### Dynamic Routing
* Routers can use dynamic routing protocols to advertise information about the routes they know to other routes.
* They form 'adjacencies' / 'neighbor relationships' / 'neighborships' with adjacent routers to exchange this information.
* If multiple routes to a destination are learned, the router determines which route is superior and adds it to the routing table. It uses the 'metric' of the route to decide which is superior (lower metric = superior).
## Types of Dynamic Routing Protocols
* Dynamic routing protocols can be divided into two main categories:
	* **IGP (Interior Gateway Protocol)**: Used to share routes within a single autonomous system (AS), which is a single organization (ie. a company).
	* **EGP (Exterior Gateway Protocol)**: Used to share routes between different autonomous systems.
![dynamic routing protocols](./img2/dynamic-routing-protocols.png)
* **EGP** is not needed for the CCNA. Just remember that it is used to share route information between autonomous systems and that **BGP** is the only **EGP** that is used in modern networks.
### Distance Vector Routing Protocols
![distance vector routing protocols routes learning process](./img2/distance-vector-routing-process.png)
* Distance vector protocols were invented before link state protocols.
* Early examples are **RIPv1** and Cisco's proprietary protocol **IGRP** (which was updated to **EIGRP**).
* Distance vector protocols operate by sending the following to their directly connected neighbors:
	* Their know destination networks.
	* Their metric to reach their known destination networks.
* This method of sharing route information is often called 'routing by rumor'. This is because the router doesn't know abut the network beyond its neighbors. It only knows the information that its neighbors tell it.
* It's called 'distance vector' because the routers only learn the 'distance' (metric) and 'vector' (direction, the next-hop router) of each route.
### Link State Routing Protocols
* When using a **link state** routing protocol, every router creates a 'connectivity map' of the network.
* To allow this, each router advertises information about its interfaces (connected networks) to its neighbors. These advertisements are passed along to other routers, until all routers in the network develop the same map of the network.
* Each router independently uses this map to calculate the best routes to each destination.
* Link state protocols use more resources (CPU, Memory) on the router because more information is shared. However, link state protocols tend to be faster in reacting to changes in the network than distance vector protocols.
## Dynamic Routing Protocol Metrics
* A router's route table contains the best route to each destination network it knows about.
* If a router using a dynamic routing protocol learns two different routes to the same destination, how does it determine which is 'best' ? It uses the **metric** value of the routes to determine which is best. A lower metric = better.
* Each routing protocol uses a different metric to determine which route is the best.
![ospf path selection](./img2/ospf-route-path-selection.png)
* Above, R1 learns two paths to `192.168.4.0/24` - one through R2 and the other through R3. However, only the route via R2 is added to the routing table. This is because the FastEthernet connection through R3 has a higher metric cost than the other Gigabit  connections through R2.
### ECMP with Dynamic Routing Protocol
![ECMP with dynamic routing protocol](./img2/ECMP-dynamic-routing.png)
* The routes were dynamically learned using the OSPF protocol as indicated in the picture.
* **ECMP (Equal Cost Multi-Path)**: If a router learns two (or more) routes via the same routing protocol to the same destination (same network address, same subnet mast) with the same metric, all routes will be added to the routing table. Traffic will be load-balanced over all the routes that formed the tie.
	* The first value of the square bracket is the administrative distance([110/]).
	* The second value of the square brackets is the metric ([/3]).
### ECMP with Dynamic Routing Protocol
![ECMP static routes](./img2/ecmp-static-routes.png)
* It's possible to have ECMP (Equal Cost Multi-Path) with static routes as well.
* As shown above, there is a tie in the metric number for the two configured routes to the same destination network. Therefore, the traffic will be load balanced between them.
	* Static routes don't really use the concept of metric so there will always be a value of 0, resulting in ties for multiple static routes to the same destination network.
### IGP (Interior Gateway Protocol) Metrics
![dynamic routing metrics](./img2/dynamic-routing-metrics.png)

The example below demonstrates the differences between the RIP and OSPF dynamic routing protocols.
![OSPF vs RIP path selection](./img2/ospv-vs-rip-path-selection.png)
* Using **RIP**, R1 will add both routes to its routing table - the route through R2 and the one through R3. This is because both routes take 2 hops to get to the destination network.
* Using **OSPF**, R1 will only add the route through R2 to its routing table because it has a lower total metric than the route through R3.
### Administrative Distance

## Administrative Distance
