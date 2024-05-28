## Wireless Network Security
* Although security is important in all networks, it is even more essential in wireless networks.
* Because wireless signals are not contained within a wire, any device within range of the signal can receive the traffic.
* In wired networks, traffic is only encrypted when sent over an untrusted network such as the Internet.
* In wireless networks, it is very important to encrypt traffic sent between the wireless clients and the AP.
## Authentication
* All clients must be authenticated  before they can associate with an AP.
* In a corporate setting, only trusted users/devices should be given access to the network.
	* In corporate settings, a separate SSID which doesn't have access to the corporate network can be provided for guest users.
* Ideally, clients should also authenticate the AP to avoid associating with a malicious AP.
* There are multiple ways to authenticate:
	* Password
	* Username/Password
	* Digital certificates installed on the device.
## Encryption
* Traffic sent between clients and APs should be encrypted so that it can't be read by anyone except the AP and the client.
* There are many possible protocols that can be used to encrypt traffic.
* All devices on the WLAN will use the same protocol, however each client will use a unique encryption/decryption key so that other devices can't read its traffic.
* A group key is used by the AP to encrypt traffic that it wants to send to all of its clients.
	* All of the clients associated with the AP keep that key so they can decrypt the traffic.
## Integrity
* Integrity helps verify that a message has not been modified by a third party.
* The message that is sent by the source host should be the same as the message that is received by the destination host.
* A **MIC (Message Integrity Check)** is added to messages to help protect their integrity.
	* There is multiple protocols that can be used to calculate this MIC. 
	* The sender and receiver must use the same protocol to calculate the MIC.

![Message integrity check process](./img4/message-integrity-check-process-MIC.png)
* If the two MICs aren't the same, that means that the message was tampered with and will be discarded.
## Wireless Authentication Methods

## Wi-Fi Protected Acces (WPA)