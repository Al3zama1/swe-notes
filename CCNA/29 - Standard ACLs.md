## What Are ACLs?
* ACLs (Access Control Lists) have multiple uses.
	* We are focusing on ACLs from a security perspective. Control who has access to different parts of the network.
* ACLs function as a packet filter, instructing the router to permit or discard specific traffic.
	* The default behavior is to forward all traffic.
* ACLs can filter traffic based on source/destination IP addresses, source/destination Layer 4 ports, etc.
## ACL Logic
![](./img2/standard-acls-topology.png)
* ACLs shouldn't be configured randomly. They must be used to achieve a certain requirement.
* ACLs are configured globally on the router (global config mode).
* They are an ordered sequence of ACEs (Access Control Entries).
* Requirement:
	* Hosts in `192.168.1.0/24` can access the `10.0.1.0/24` network.
	* Hosts in `192.168.2.0/24` cannot access the `10.0.1.0/24` network.
* ACL 1: requirement satisfaction
	* If source IP = `192.168.1.0/24`, then permit.
	* If source IP = `192.168.2.0/24`, then permit.
	* If source IP = any, then permit.

* Configuring an ACL in global configuration mode will not make the ACL take effect.
* The ACL must be applied to an interface.
* ACLs are applied either inbound or outbound.
## ACL Types
## Standard Numbered ACLs
## Standard Named ACLs
