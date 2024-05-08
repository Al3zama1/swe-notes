## Correction (IPv6 Address Representation)
* RFC 5952 is '**A Recommendation for IPv6 Address Text Representation**'.
* Before this RFC, IPv6 address representation was more flexible.
	* You could remove leaning 0s, or leave them.
	* You could replace all-0 quartets with ::, or leave them.
	* You could use upper-case 0xA, B, C, D, E, F or lower-case 0xa, b, c, d, e, f.
* RFC 5952 suggests standardizing IPv6 address representation.
	* Leading 0s must be removed.
	* `::` must be used to shorten the longest string of all-0 quartets. 
		* Don't use `::` if there is only one all-0 quartet.
		* If there are two equal-length choices for the `::`, use it to shorten the one on the left.
	* Hexadecimal character a, b, c, d, e, and f must be written using lower-case.
## IPv6 Header
![IPv6 header](./img2/ipv6-header.png)
* The IPv6 header has a fixed size of 40 bytes compared to the IPv4 header (20 - 60 bytes).
* **Version**: 
	* 4 bits in length.
	* Indicates the version of IP that is used.
	* Fixed value of 6 (0b0110) to indicate IPv6.
* **Traffic Class**:
	* 8 bits in length.
	* Used for QoS (Quality of Service) to indicate high-priority traffic.
	* For example, IP phone traffic, live video calls, etc, will have a Traffic Class value which gives them priority over other traffic.
* **Flow Label**:
	* 20 bits in length.
	* Used to identify specific traffic 'flows' (communication between a specific source and destination).
* **Payload Length**:
	* 16 bits in length.
	* Indicates the length of the payload (the encapsulated Layer 4 segment) in bytes.
	* The length of the IPv6 header itself isn't included because it's always 40 bytes.
* **Next Header**:
	* 8 bits in length.
	* Indicates the type of the 'next header' (header of the encapsulated segment). For example, TCP or UDP.
	* Same function as the IPv4 header's 'Protocol' field.
* **Hop Limit**:
	* 8 bits in length.
	* The value in this field is decremented by 1 by each router that forwards it. If it reaches 0, the packet is discarded.
	* Same function as the IPv4 header's TTL field.
* **Source/Destination Address**: 
	* 128 bits each.
	* These fields contain the IPv6 addresses of the packet's source and the packet's intended destination.
## Solicited-Node Multicast Address
* 
## Neighbor Discovery Protocol (NDP)
## SLAAC
## IPv6 Static Routing
