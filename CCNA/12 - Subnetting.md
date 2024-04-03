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