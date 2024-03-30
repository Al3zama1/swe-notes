
## Switch Interfaces Default Status
```
SW1>enable
SW1#show ip interface brief
Interface       IP-Address     OK?     Method     Status    Protocol
FastEthernet0/1 unassigned     YES     unset      up        up
FastEthernet0/2 unassigned     YES     unset      down      down
```

* Router interfaces have the `shutdown` command applied by default.
	*  Will be in the `administratively down/down (status/protocol)` state by default.
* Switch interfaces do not have the `shutdown` command applied by default.
	* Will be in the `up/up(status/protocol)` state if connected to another device.
	* Will be in the `down/down` state if not connected to another device.

```
SW1#show interfaces status
Port   Name     Status         Vlan    Duplex     Speed   Type
Fa0/1           connected      1       a-full    a-100  10/100BaseTX
Fa0/1           notconnected   1       a-full    auto   10/100BaseTX
```
* Name field is the interface description.
* Duplex indicates whether the device is capable of sending and receiving data at the same time.
	* Duplex is auto by default on Cisco switches. It will negotiate with the connected device and use full-duplex if possible.
	* a-full means that full-duplex was automatically negotiated with the connected device.
* Speed is negotiated automatically by default. The interfaces shown above are fast ethernet interfaces so they are capable of speeds of 10Mbps and 100 Mbps.
	* The switch will automatically negotiate the speed and pick the highest speed possible by both, the device and the interface that it is connected to.
	* a-100 in this case means that a speed of 100Mbps was automatically negotiated between the device and the interface it is connected to. 
* 