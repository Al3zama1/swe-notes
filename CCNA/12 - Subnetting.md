## IPv4 Address Assignment
* The IANA (Internet Assigned Numbers Authority) assigns IPv4 addresses/networks to companies based on their size.
* For example, a very large company might receive a **class A** or **class B** network, while a small company might receive a **class C** network.
* However, this led to many wasted IP addresses.
#### IP Address Waste
![example of wasted IP addresses](./img/ip-address-waste.png)
* The network connecting the San Francisco and New York offices of a corporation is a `point-to-point network`. Its only purpose is to connect the two corporation offices.
* Even when the network (class C) with the least number of addresses for hosts is picket, 252 addresses are unused.

#### IP Address Waste
* Company X needs IP addressing for 5000 end hosts.
* A **class C** network does not provide enough addresses, so a **class B** network must be assigned.
* This will result in about 60000 addresses being wasted.


## CIDR (Classless Inter-Domain Routing)
* When the internet was first created, the creators did not predict that the internet would become as large as it is today.
* This resulted in wasted address space like the examples above. Now a days IP address exhaustion has become a problem because there is not enough addresses.
* The IETF (Internet Engineering Task Force) introduces CIDR in 1993 to replace the 'classful' addressing system. This remedies the issue of wasted addresses.
* CIDR removed the requirements of prefix length set by the different network classes.
	* Class A = /8
	* Class B = /16
	* Class C = /24
* This allowed larger networks to be split into smaller networks, allowing greater efficiency.
	* These smaller networks are called `subnetworks` or `subnets`. 
* Unfortunately we can't always make subnets have exactly the number of addresses we need. That is fine because it provides room for growth in the future.

==**The process of subnetting Class A, Class B, and Class C networks is EXACTLY THE SAME.**==
$$
Number\ of\ Subnets\ Possible:\ 2^x, x = number\ of\ borrowed\ host\ bits
$$

#### Subnets/Hosts (Class C)
How many usable addresses are there in each network?
* 203.0.113.0/25
	* 7 host bits = 128 total addresses.
	* (2^7) - 2 = 126 usable addresses.
	* 1 borrowed host bit makes 2 subnets possible.
	* Subnet mask = 255.255.255.128
* 203.0.113.0/26
	* 6 host bits = 64 total addresses.
	* (2^6) - 2 = 62 usable addresses.
	* 2 borrowed host bit makes 4 subnets possible
	* Subnet mask = 255.255.255.192
* 203.0.113.0/27
	* 5 host bits = 32 total addresses.
	* (2^5) - 2 = 30 usable addresses.
	* 3 borrowed host bit makes 8 subnets possible.
	* Subnet mask = 255.255.255.224
* 203.0.113.0/28
	* 4 host bits = 14 total addresses.
	* (2^4) - 2 = 14 usable addresses..
	* 4 borrowed host bit makes 16 subnets possible.
	* Subnet mask = 255.255.255.240
* 203.0.113.0/29
	* 3 host bits = 8 total addresses.
	* (2^3)  - 2 = 6 usable addresses.
	* 5 borrowed host bit makes 32 subnets possible.
	* Subnet mask = 255.255.255.248
* 203.0.113.0/30
	* 2 host bits = 4 total addresses.
	* (2^2) - 2 = 2 usable addresses.
	* 6 borrowed host bit makes 64 subnets possible.
	* Subnet mask = 255.255.255.252
* 203.0.113.0/31
	* 1 host bit = 2 total addresses.
	* (2^1) - 2 = 0 usable addresses.
	* 7 borrowed host bit makes 128 subnets possible.
	* Subnet mask = 255.255.255.254
	* For a point-to-point connection like the one shown above it is possible to use  a /31 mask and is recommended.
		* Normally it would not be possible because there would leave no addresses for the network and broadcast addresses.
		* However, for a dedicated point-to-point connection, there is really no need for the network and broadcast addresses.
		* Routers will give the following warning when using /31 mask: `Warning: use /31 mask on non point-to-point interfaces cautiously`.
* 203.0.113.0/32
	* 0 host bit = 0 total addresses.
	* (2^0) - 2 = -1 usable addresses.
	* 8 borrowed host bit makes 256 subnets possible.
	* Subnet mask = 255.255.255.255
	* Will probably never use a /32 mask to configure an actual interface. However, there are some uses for a /32 mask.
	* a /32 mask can be used when you want to create a static route not a network, but just to one specific host.

This is called subnetting because we are only using a subset of the total available addresses in the address class that we are working on. In this case we are creating subnets for a class C network.
![subnet class C network](./img/CIDR-Notation-24.png)


