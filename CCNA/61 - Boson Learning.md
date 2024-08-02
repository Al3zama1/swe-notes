## IP Phones Trust
The command moves the trust boundary from the switch to the IP phone, which lets the switch accept the IP phone voice traffic as having come from a trusted source.
```
mls qos trust cost
```

The switch instructs the IP phone connected to the interface to trust the CoS priority of incoming data packets. The IP phone will not override the CoS values from the host and will accept the existing CoS values as valid and forward unchanged data packets to the switch.
```
SW(config-if)switchport priority extend trust
```

The switch instructs the IP phone to reclassify the CoS priority value that the host assigns to its data packets. It will override the CoS priority value assigned by the host and tags the data packets with a CoS of 0.

Overriding the CoS priority value ensures that voice packets will have a higher priority than the data packets. Therefore, voice packets will be given preference over the data packets as they are processed by the switch.
```
SW(config-if)switchport priority extend cos
```

## 802.11 Standards
### 802.11k
Provides assisted roaming in a wireless network. A roaming wireless client can request a list of known neighboring APs that might be potential candidates for transition. The list returned by an AP is optimized for the client and contains only APs in the same wireless band with which the client is associated. This enables the client to find a new AP without needing to probe unnecessary wireless channels, which speeds transition and increases battery life for portable devices.

### 802.11r 
Provides support for fast transition (FT) roaming. A wireless client and an AP perform the Pairwise Master Key (PMK) calculation in advance. These recalculated PMK keys are then used after the client sends its re-association request to the new AP and the AP responds with its association response. It enables the client to transition to a new AP without needing to re-authenticate, thereby  speeding the handover between APs and minimizing adverse QoS effects caused by roaming.

### 802.11w
Provides management frame protection (MFP). MFP is a security mechanism that prevents management frames from being compromised by a malicious user.

### 802.11v
Provides network-assisted power saving. A wireless client can remain in a standby or sleep state longer to improve battery life. 802.11v provides a Directed Multicast Service (DMS), which enables a client to request that certain multicast messages be delivered as unicast messages instead. This enables the client to ignore the multicast messages during sleep and to receive the unicast messages at a greater rate of speed once it is active again. It also provides clients the ability to extend the amount of time they may remain idle before being disassociated with an AP.

## Access/Configure WLC Though HTTPS

Configure a WLC to support HTTPS management connections. This is allowed by default, so it must only be used if it has been previously disabled.
```
config network secureweb enable
```


## Device Password

Enter a plain text password that should be converted to an MD5 hash and stored.
```
username boson secret eX$1mM@x
```

If you already now the hash value of the password, you can use the MD5 hash value of a password manually instead of assigning a plain-text password to be converted into a hash by the IOS.
* The `5` parameter indicates that the assigned value is already in MD5 hash form.
```
username boson secret 5 eX$1mM@x
```

## Multicast MAC Address
The Ethernet multicast range of 0100:5E00:0000 - 0100:5E7F:FFFF has been allocated for IP multicast use. This means that the first 24 bitts of a 48-bit multicast MAC address are always 0100:5E, and the twenty-fifth bit is always set to 0. The remaining 23 bits are created from the last 23 bits of the multicast IP address.
* The right most bit is indicates whether the MAC address is unicast or multicast.
	* 0 - unicast
	* 1 - multicast
* The second right most bit indicates whether the address was globally or locally assigned.
	* 0 - Globally administered (OUI).
	* 1 - Locally administered.