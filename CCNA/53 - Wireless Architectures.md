## 802.11 Messages/Frame Format
![802.1ll frame format](./img4/802-11-frame-format.png)
* 802.11 frames have a different format than 802.3 Ethernet Frames.
	* They are more complicate than Ethernet frames.
	* For the CCNA you don't have to learn it in as much detail as the Ethernet and IP headers.
* Depending on the 802.11 version and the message type, some of the fields might not be present in the frame.
	* For example, there are 4 different Address fields, but not all messages use all 4 Address fields.
* **Frame Control**: Provides information such as the message type and subtype.
* **Duration/ID**: Depending on the message type, this field can indicate:
	* The time (in microseconds) the channel will be dedicated for transmission of the frame.
	* An identifier for the association, the connection between the wireless client and AP.
* **Addresses**: Up to four addresses can be present in an 802.11 frame. Which addresses are present, and their order, depends on the message type.
	* Destination Address (DA): Final recipient of the frame.
	* Source Address (SA): Original sender of the frame.
	* Receiver Address (RA): Immediate recipient of the frame, but not necessarily the final destination.
	* Transmitter Address (TA): Immediate sender of the frame, but not necessarily the original sender, the original source of the frame.
* **Sequence Control**: Used to reassemble fragments and eliminate duplicate frames.
* **QoS Control**: Used in QoS to prioritize certain traffic.
* **HT (High Throughput) Control**: Added in 802.11n to enable High Throughput operations.
	* 802.11n is also known as High Throughput (HT) Wi-Fi.
	* 802.11ac is also known as Very High Throughput (VHT) Wi-Fi.
* **FCS (Frame Check Sequence)**: Same as in an Ethernet frame, used to check for errors.
## 802.11 Association Process
* Access Points bridge traffic between wireless stations/clients and other devices.
* For a station/client to send traffic through the AP, it must be associated with the AP.
* There are three 802.11 connection states:
	* Not authenticated, not associated.
	* Authenticated, not associated.
	* Authenticated and associated.
## Wireless AP Architectures
### Autonomous APs
### Lightweight APs
### Cloud-Based APs

## Wireless LAN Controller (WLC) Deployments
