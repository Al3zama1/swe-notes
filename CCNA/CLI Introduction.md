**How to connect to a Cisco device console**? 
* USB Mini-B
* RJ-45 with Rollover cable

**Terminal Serial Connection Settings**
* Speed: 9600
* Data bits: 8
* Stop bits: 1
* Parity: none
* Flow control: none

**CLI Modes**
* User EXEC Mode 
	* Denoted by a > symbol.
	* very limited.
	* Users can look at some things, but can't make any changes to the configuration.
* Privileged EXEC Mode
	* Denoted by a # symbol
	* provides complete access to view the device's configuration, restart the device, etc.
	* Cannot change the configuration, but can change the time on the device, save the configuration file, etc.
* Global Configuration Mode
	* Make changes to the configuration.

```
Enter Privileged EXEC Mode
Router> enable
Router#

Exit Privileged EXEC Mode
Router# disable
Router>


Enter Global Configuration Mode
Router#configure terminal
Router(config)#

Exit Global Configuration Mode
Router(config)# end/exit
```

**Enable Password**
* `Router(config)enable password <your-password>`
	* passwords are not encrypted

**Enable Password Encryption**
* `Router(config)#service password-encryption` will encrypt unencrypted passwords and future passwords.
* It used type 7 encryption.
* `enable secret is not affected.`

**Disable Password Encryption**
* `Router(config)#no password-encryption` will deactivate password encryption.
* Current encrypted passwords will not be decrypted.
* Future passwords will not be encrypted.
* `enable secret` is not affected.

**Enable Secret**
* `Router(config)# enable secret <secret>` will set encrypted password for the device.
* It has a more secure encryption mechanism, MD5 type encryption.
* If both secret and password are set, secret takes precedence.
* The `service password-encryption` has no effect on secret.

**Configuration Files**
* Running configuration is the current, active configuration file on the device. As you enter commands in the CLI, you edit the active configuration.
	* `Router# show running-config` shows the configuration.
* Startup configuration is the configuration file that will be loaded upon restart of the device.
	* `Router#show startup-config` shows the configuration.

**Save The Configuration Methods**
* save
* save memory
* copy running-config startup-config