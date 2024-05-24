## Classification/Marking
* The purpose of QoS is to give certain kinds of network traffic priority over others during congestion.
* **Classification** organizes network traffic (packets) into traffic classes (categories).
* Classification is fundamental to QoS. To give priority to certain types of traffic, you have to identify which type of traffic to give priority to.
* There are many methods of classifying traffic.
	* An ACL. Traffic which is permitted by the ACL will be given certain treatment, other traffic will not.
	* **NBAR (Network Based Application Recognition)** performs a deep packet inspection, looking beyond the Layer 3 and Layer 4 information up Layer 7 to identify the specific kind of traffic.
	* In the Layer 2 and Layer 3 headers, there are specific fields used for this purpose.
* The **PCP (Priority Code Point)** field of the 802.1Q tag (in the Ethernet header) can be used to identify high/low priority traffic.
	* Can only be used when there is a dot1q tag! 
		* Available in trunk links since traffic is tagged, unless it is in the native VLAN.
		* Available in access links with a voice VLAN since voice traffic is tagged.
* The **DSCP (Differentiated Service Code Point)** field of the IP header can also be used to identify high/low priority traffic.
### QoS Classification at Layer 2 (PCP/CoS)
![QoS classification at Layer 2](./img3/QoS-classification-layer2.png)
* To **mark** (QoS term) traffic is to set the value in the PCP or DSCP fields. Then, network devices look at those markings and use them to classify the traffic as high/low priority. 
### QoS Classification at Layer 3 (DSCP)
* RFC 2474 (1998) defines the DSCP field, and other 'DiffServ' RFCs elaborate on its use.
* With IPP updated to DSCP, new standard markings had to be decided upon.
	* By having generally agreed upon standard markings for different kinds of traffic, QoS design & implementation is simplified, QoS works better between ISPs and enterprises, among other benefits.
* You should be aware of the following standard markings:
	* Default Forwarding (DF) - best effort traffic.
	* Expedited Forwarding (EF) - low loss/latency/jitter traffic (usually voice).
	* Assured Forwarding (AF) - set of 12 standard values.
	* Class Selector (CS) - set of 8 standard values, provides backward compatibility with IPP.
## Queuing/Congestion Management
## Shaping/Policing
