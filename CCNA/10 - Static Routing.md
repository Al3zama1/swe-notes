Static routes enable routers to send packages to remote destinations that are aren't directly connected to the router itself.

## Routing Packets: Default Gateway
* End hosts can send packets directly to destinations in their connected network.
* To send packets to destinations outside of their local network, they must send the packets to their **default gateway/route**.
	* It is a route to 0.0.0.0/0 with all netmask bits set to 0. Includes all addresses from 0.0.0.0 to 255.255.255.255.
	* The default route is the least specific route possible, because it includes all IP addresses. Any packet that does not match any more specific address will be sent here.