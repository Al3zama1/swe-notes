The header is read left to right, top to bottom. Top left being the first bit and bottom right being the last bit in the header.
![IPv4 header](./img/ipv4-header.png)
* **Version**: Identifies the version of IP used. The IPv4 and IPv6 headers have different structures.
	* Length of 4 bits
	* IPv4 = 4 (0100)
	* IPv6 = 6 (0110)
* **IHL (Internet Header Length)**: The final field of the IPv4 header (Options) is variable in length, so this field is necessary to indicate the total length of the header.
	* Length of 4 bits.
	* Identifies the length of the header in 4-byte increments. A value of 5 means the size is 20 bytes.
	* Minimum IPv4 header length is 20 (value 5) bytes with empty Options field.
	* Maximum IPv4 header length is 60 (value 15) bytes with maximum length Options field.
		* The maximum size of the IP Options field is 40 bytes
* **DSCP (Differentiated Services Code Point)**:
	* Length of 6 bits.
	* Used for QoS (Quality of Service).
	* Used to prioritize delay-sensitive data (streaming voice, video, etc).
* **ECN (Explicit Congestion Notification)**: Provides end-to-end (between two points) notifications of network congestion without dropping packets.
	* Length of 2 bits.
	* Without ECN, congestion in a network is usually signaled by dropping packets.
	* It's an optional feature that requires both endpoints, as well as the underlying network infrastructure to support it.
* **Total Length**: Indicates the total length of the packet (L3 header + L4 segment).
	* Length of 16 bits.
	* Measured in bytes.
	* Minimum value of 20 bytes (IPv4 header with no encapsulated data).
	* Maximum value of 65,535 bytes (maximum 16-bit value).
* **Identification**: If a packet is fragmented due to being too large, this field is used to identify which packet the fragment belongs to.
	* Length of 16 bits.
	* All fragments of the same packet will have their own IPv4 header with the same value in this field.
	* Packets are fragmented if larger than the MTU (Maximum Transmission Unit), which is 1500 bytes.
	* Fragments are reassembled by the receiving host.
* **Flags**: Used to control and identify fragments.
	* Length of 3 bits.
	* Bit 0 is reserved, always set to 0.
	* Bit 1 is the don't fragment (DF bit), used to indicate a packet that should not be fragmented.
	* Bit 2 is the more fragments (MF bit), set to 1 to indicate more fragments in the packet and 0 to indicate the last frame.
		* Unfragmented packets will always have their MF bit set to 0 since there are no fragments.
	* Bit of 0 means `Not set`
	* Bit of 1 means `Set`
* **Fragment Offset Field**: Indicate the position of the fragment within the original, unfragmented IP packet.
	* Length of 13 bits
	* Allows fragmented packets to be reassembled even if the fragments arrive out of order.
* **Time To Live**: A router will drop a packet with a TTL of 0.
	* Length of 8 bits.
	* Used to prevent infinite loops, avoiding heavy traffic congestion.
	* Originally designed to indicate the packet's maximum lifetime in seconds.
	* In practice, indicates a 'hop count': Each time the packet arrives at a router, the router decreases the TTL by 1.
	* The recommended default TTL is 64.
* **Protocol**: Indicates the protocol of the encapsulated L4 PDU.
	* Length of 8 bits.
	* Value of 6 indicate TCP.
	* Value of 17 indicate UDP.
	* Value of 1 indicate ICMP.
	* Value of 89 indicate OSPF (dynamic routing protocol).
* **Header Checksum**: A calculated checksum used to check for errors in the IPv4 header.
	* Length of 16 bits.
	* When a router receives a packet, it calculates the checksum of the header and compares it to the one in this field of the header.
		* If they do not match, the router drops the packet.
	* Used to check for errors only in the IPv4 header.
	* IP relies on the encapsulated protocol to detect errors in the encapsulated data.
		* Both TCP and UDP have their own checksum fields to detect errors in the encapsulated data.
* **Source IP Address**: IPv4 address of the sender of the packet.
	* Length of 4 bytes (32 bits).
* **Destination IP Address**: IPv4 address of the intended receiver of the packet.
	* Length of 4 bytes (32 bits).
* **Options**: Optional field.
	* Can be 0 - 40 bytes (0 - 320 bits) in length
	* Rarely used.
	* If the IHL field is greater than 5, it means that Options are present.

