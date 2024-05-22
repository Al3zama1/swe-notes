## The Purpose of FTP/TFTP
* FTP (File Transfer Protocol) and TFTP (Trivial File Transfer Protocol) are industry standard protocols used to transfer files over a network.
* They both use a client-server model.
	* Clients can use FTP or TFTP to copy files from a server.
	* Clients can use FTP or TFTP to copy files to a server.
* AS a network engineer, the most common use of FTP/TFTP is in the process of upgrading the operating system of a network device.
* You can use FTP/TFTP to download the newer version of IOS from a server, and then reboot the device with the new IOS image.
## TFTP
* TFTP was first standardized in 1981.
* Named 'Trivial' because it is simple and has only basic features compared to FTP.
	* Only allows a client to copy a file to or from a server.
* Was released after FTP, but is not a replacement of FTP. It is another tool used when lightweight simplicity is more important than functionality.
* No authentication (username/PW), so servers will respond to all TFTP requests.
* No encryption, so all data is sent in plan text.
* Best used in a controlled environment to transfer small files quickly.
* TFTP servers listen on **UDP PORT 69**.
	* UDP is connectionless and doesn't provide reliability with transmissions. However, TFTP has similar built-in features within the protocol itself.
### TFTP Reliability
![TFTP reliability](./img3/TFTP-reliability.png)
* Every TFTP data message is acknowledged.
	* If the client is transferring a file to the server, the server will send Ack messages.
	* If the server is transferring a file to the client, the client will send Ack messages.
* Timers are used, and if an expected message isn't received in time, the waiting device will resend its previous message again.
	* TFTP uses 'lock-step' communication. The client and server alternately send a message and then wait for a reply (retransmissions are sent as needed).
	* This method of reliability isn't as efficient as TCP's forward acknowledgment and sliding window, but gets the job done
### TFTP Connections
![TFTP connections](./img3/TFTP-connections.png)
* TFTP file transfers have three phases:
	* **Connection**: TFTP client sends a request to the server, and the server responds back, initializing the connection.
	* **Data Transfer**: The client and server exchange TFTP messages. One sends data and the other sends acknowledgements.
	* **Connection Termination**: After the last data message has been sent, a final acknowledgement is sent to terminate the connection.
### TFTP TID
This is beyond the scope of the CCNA

![TFTP TID](./img3/TFTP-TID.png)
* When the client sends the first message to the server, the destination port is UDP 69 and the source is a random ephemeral port.
* This random port is called a **Transfer Identifier (TID)** and identifies the data transfer.
* The server then also selects a random TID to use as the source port when it replies, not 69.
* When the client sends the next message, the destination port will be the server's TID, not 69.
## FTP
* FTP was first standardized in 1971.
* FTP uses TCP ports 20 and 21.
* Username and passwords are used for authentication, however there is no encryption.
* For greater security, FTPS (FTP over SSL/TLS) can be used.
	* An upgrade to FTP.
* SSH File Transfer Protocol (SFTP) can also be used for grater security.
	* An entirely new protocol.
* FTP is more complex than FTP and allows not only file transfers, but clients can also navigate file directories, add and remove directories, list files, etc.
* The client sends FTP commands to the server to perform these functions.
### FTP Control Connections

## FTP/TFTP Functions & Differences

## IOS File Systems

## Using FTP/TFTP in IOS
