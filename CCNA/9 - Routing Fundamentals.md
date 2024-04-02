## What is Routing ?
Routing is the process that routers use to determine the path that IP packets should take over a network to reach their destination.
* Routers store routes to all of their known destinations in a **routing table**. 
* When routers receive packets, they look in the routing table to find the best route to forward the packet.

## Routes Learning Mechanism
* **Dynamic Routing**: Routers use dynamic routing protocols (ie. OSPF) to share routing information with each other automatically and build their routing tables.
* **Static Routing**: A network engineer/admin manually configures routes on the router.

## Where Do Routers Send Packages ?
* Packages are sent to the **next-hop** (the next router in the path to the destination) when the router is not directly connected to the destination network.
* Packages are sent to the destination device when the router is directly connected to the destination network.
* Routers keep packages when the destination is the router's IP address.