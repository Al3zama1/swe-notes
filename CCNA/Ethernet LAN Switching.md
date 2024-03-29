## Ethernet Frame

![ethernet frame structure](./img/ethernet-frame.png)
**The size of ethernet frames is 26 bytes (header + trailer)**
#### Preamble
* 7 bytes (56 bits) field length.
* Alternating 1's and 0's.
	* 10101010 * 7
* Allows devices to synchronize their receiver clocks.
#### SFD (Start Frame Delimiter)
* 1 byte (8 bits) field length.
* Alternating 1's and 0's.
	* 10101011
* Marks the end of the preamble and the beginning of the rest of the frame.
#### Destination/Source
* 6 bytes (48 bits) field length
* Indicate the device sending and receiving the frame.
* Consist of the destination and source `MAC(Media Access Control) address`.
	* Address of the physical device.
#### Type/Length
* 2 bytes (16 bits) field length.
* A value of `1500 or less` in this field indicates the `length` of the encapsulated packet (in bytes).
* A value of `1536 or greater` in this field indicates the `type` of the encapsulated packet (usually IPv4 or IPv6, ARP, etc...) and length is determined via other methods.
* `IPv4`: 0x0800 hexadecimal and 2048 in decimal.
* `IPv6`: 0x86DD hexadecimal and 34525 decimal. 
#### FCS (Frame Check Sequence)
* 4 bytes (32 bits) field length.
* Detects corrupted data by running a `CRC(Cyclic Redundancy Check)` algorithm over the received data.



## MAC Address
* 6-byte (48 bits) physical address assigned to the device when it is made.
* A.K.A `Burned-In Address(BIA)`
* It is globally unique.
* Written as 12 hexadecimals characters.
* The first 3 bytes are OUI (Organizationally Unique Identifier), which is assigned to the company making the device.
* The last 3 bytes are unique to the device itself.

## Switch Functionality
* Switches `learn`, `flood`, and `fordward` packets
	* **Learn**
		* Switches dynamically learn MAC addresses when a new frame arrives. The association between the source MAC address of the packet and the interface that it came is is written to the switch's `MAC Address Table`.
		* `Aging`: Associations in a switch's MAC address table are removed after 5 minutes of inactivity.
		* `Dynamic MAC address` is an address that is learned automatically by the switch.
	* **Flood**
		* `Unknown unicast frames` are flooded out all interfaces except the one where it came.
		* `Broadcast frames` are flooded out all interfaces except the one where it came.
	* **Fordward**
		* `Known unicast frames` are forwarded out the switch interface associated with the destination MAC address.