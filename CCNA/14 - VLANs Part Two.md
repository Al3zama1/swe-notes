## Native VLAN on a Router (ROAS)
* Traffic in the native VLAN is more efficient because frames are not tagged, making them smaller. As a result, more frames can be sent per second.

#### Native VLAN Configuration on a Router
There are 2 methods of configuring the native VLAN on a router:
* Use the command `encapsulation dot1q vlan-id native ` on the router.
* Configure the IP address for the native VLAN on the router's physical interface (the `encapsulation dot1q vlan-id` command is not necessary)
	* This method does not use a subinterface at all.

```
R1(config)#interface g0/0.10
R1(config-subif)#encapsulation dot1q 10 native
R1(config-subif)#
```


