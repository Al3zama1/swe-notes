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

