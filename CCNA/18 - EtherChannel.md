## Why is EtherChannel Needed?
* ***Access Layer Switch**: A switch that end hots connect to.
* ***Distribution Layer Switch**: A switch that access layer switches connect to.
* ***Oversubscription**: The bandwidth of the interfaces connected to end hosts is greater than the bandwidth of the connection to the distribution switch(es). Some oversubscription is acceptable, but too much will cause congestion.

![](./img2/asw-to-dsw-with-multiple-links.png)

Let's say there are many end hosts connected to an access switch(ASW1) and they are all trying to access the internet to do their work. The network administrator notices that the connection to the distribution switch(DSW1) 
is congested, so he decides to add another link to increase the bandwidth and be able to support all the end hosts. However, the additional link doesn't seem to help. The connection between ASW1 and DSW1 is still congested and end users are reporting problems. Therefore, the admin decides to add another link between ASW1 and DSW1. The total bandwidth of the connections to the end hosts is still greater than the bandwidth of the connection to DSW1, but that's okay because not all hosts in the network are always in a constant state of sending and receiving internet traffic.

Despite the addition of multiple links between ASW1 and DSW1, the connection between the two switches is just as congested as it was with a single link.
* If you connect two switches together with multiple links, all except one will be disabled by spanning tree.
* If all of ASW1's interfaces were forwarding, Layer 2 loops would form between ASW1 and DSW1, leading to broadcast storms.
* Other links will be unused unless the active link fails. In that case, on of the inactive links will start forwarding.

## EtherChannel
* ***EtherChannel** allows you to group multiple physical interfaces into a group which operates as a single logical interface.
* STP will treat this group as a single interface, therefore none of theme will be disabled.
* Traffic in the EtherChannel will be load balanced among the physical interfaces in the group. An algorithm is used to determine which traffic will use which physical interface.
	* The bandwidth of separate interfaces is combined to form a faster virtual interface. For example, a group of four 1GB interfaces combined with EtherChannel form a faster virtual 4GB interface.
