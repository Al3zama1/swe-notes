## Dynamic NAT
* In **dynamic NAT**, the router dynamically maps *inside local* addresses to *inside global* addresses as needed.
	* It clears the mappings when they are no longer needed.
* An ACL is used to identify which traffic should be translated.
	* If the source IP is **permitted** by the ACL, the source IP will be translated.
	* If the source IP is **denied** by the ACL, the source IP will not be translated.
		* The traffic will not be dropped though. The ACL is simply being used to identify which traffic should be translated.
* A NAT pool is used to define the available *inside global* addresses.
* Although they are dynamically assigned, the mappings are still one-to-one (one *inside local* IP address per *inside global* IP address).
* If there aren't enough *inside global* IP addresses available (all are currently being used), it is called 'NAT pool exhaustion'.
	* If a packet from another inside host arrives and needs NAT but there are no available addresses, the router will drop the packet.
	* The host will be unable to access outside networks until one of the *inside global* IP addresses becomes available.
		* Dynamic NAT entries will time out automatically and become available if not used, or you can clear them manually.
## Dynamic PAT


