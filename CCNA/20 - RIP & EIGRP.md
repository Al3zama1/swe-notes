## Routing Information Protocol (RIP)
* It's an industry standard protocol.
* Distance vector IGP (uses routing-by-rumor logic to learn/share routes).
* Uses hop count as its metric. One router = one hop (bandwidth is irrelevant).
* The maximum hop count is 15 (anything more than that is considered unreachable).
* RIP is almost never used in real networks, but it can possibly be used in small networks and lab environments.
* There is 3 versions:
	* **RIPv1** and **RIPv2** is used for IPv4.
	* **RIPng** (RIP Next Generation) used for IPv6 (Not needed for CCNA).
* Uses two message types:
	* **Request**: To ask RIP-enabled neighbor routers to send their routing table.
	* **Response**: To send the local router's routing table to neighboring routers.
* By default, RIP-enabled routers will share their routing table every 30 seconds.
	* This can cause problems in networks with lots of routers, as these regular updates can clog up the network.

### RIPv1
* Only advertises classful addresses (Class A, Class B, Class C). However, classful addresses are no longer used in modern networks. Don't use this version if you are going to use RIP.
* Doesn't support VLSM and CIDR.
* Doesn't include subnet mast information in advertisements (Response messages).
	* 10.1.1.0/24 will become 10.0.0.0 (Class A address, so assumed to be /8).
	* 172.16.192.0/18 will become 172.16.0.0 (Class B address, so assumed to be /16).
	* 192.168.1.4/30 will become 192.168.1.0 (Class C address, so assumed to be /24).
* Messages are broadcast to 255.255.255.255
### RIPv2
* Supports VLSM and CIDIR.
* Use this version if you are going to use RIP.
* Includes subnet mast information in advertisements (Response messages).
* Messages are **multicast** to 224.0.0.9.
	* **Broadcast**: Messages are delivered to all devices on the local network.
	* **Multicast**: Messages are delivered only to devices that have joined that specific multicast group.

### RIP Configuration
* RIP configuration is not on the CCNA. It is really simple to do and will serve as a good introduction to dynamic routing.
```
R1(config)#router rip
R1(config-router)#version 2
R1(config-router)#no auto-summary
R1(config-router)#network 10.0.0.0
R1(config-router)#network 172.16.0.0
```
* `R1(config-router)#no auto-summary` disables auto-summary, which is on by default. auto-summary automatically converts the networks the router advertises to classful networks.
	* For example, the 172.16.1.0/28 network attached to R1 is a class B network. Therefore, it would be advertised as 172.16.0.0/16.
## Enhanced Interior Gateway Routing Protocol (EIGRP)
