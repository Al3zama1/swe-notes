## Intro to Layer 2 Discovery Protocols
![Layer 2 discovery protocols interaction](./img2/layer-2-discovery-protocols-interaction.png)
* Layer 2 discovery protocols such as **CDP** and **LLDP** share information with and discover information about neighboring (connected) devices.
* These protocols operate at Layer 2, they don't use IP addresses. However, they can be used to share layer 3 information such as IP addresses too.
* The shared information includes host name, IP address, device type, etc.
* CDP is a Cisco proprietary protocol.
* LLDP is an industry standard protocol (IEEE 802.1AB).
* Because they share information about the devices in the network, they can be considered a security risk and are often not used. It is up to the network engineer/admin to decide if they want to use them in the network or not.
## Cisco Discovery Protocol (CDP)
## Link Layer Discovery Protocol (LLDP)
