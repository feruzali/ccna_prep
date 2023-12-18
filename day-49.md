---
description: Port Security
---

# Day 49

### Port Security

Port Security is a security feature of Cisco switches. It allows to control which source MAC addresses are allowed to enter the switchport. If an unauthorised source MAC address enters the port, the action is taken. The default action is to place the interface in an err-disabled state.&#x20;

<figure><img src=".gitbook/assets/image (2) (1) (1) (1).png" alt="port security demo" width="563"><figcaption></figcaption></figure>

When port security is enabled on an interface with the default settings, one MAC address is allowed. The allowed MAC address can be configured manually. If not configured, the switch allows the first source MAC address that enters the interface. The number of MAC addresses allowed on an interface can also be configured. A combination of manually configured MAC addresses and dynamically learned addresses is also possible.

To enable port security on an interface, enter the command `switchport port-security` from the interface config mode. Note that, port security can only be enabled on access and trunk ports so they must be statically configured first. To check the port security configuration, use the command `show port-security`, for the particular interface add `interface` followed by the interface number.&#x20;

To re-enable an interface from the err-disabled state, first, the unauthorized device should be disconnected and the interface should be restarted using `shutdown` and `no shutdown` commands.&#x20;

### Secure MAC addresses

To specify the allowed MAC address, enter the command `switchport port-security mac-address` followed by the MAC address. The allowed MAC address is called a secure MAC address.  To view the secure MAC addresses, enter the command `show mac address-table secure`. By default, secure MAC addresses don't age out. But it can be changed with the command `switchport port-security aging time` followed by the time in minutes. There are two types of aging:

* **Absolute** - the default aging type. After the secure MAC address is learned, the aging timer starts and the MAC address is removed after the timer expires.
* **Inactivity** - after the secure MAC address is learned, the aging timer starts but is reset every time a switch receives a frame with that source MAC address.&#x20;

The aging type can be configured with the command `switchport port-security aging type` followed by the type. Statically configured secure MAC addresses don't age out by default. To enable it - `switchport port-security aging static`.

### Sticky secure MAC addresses

To make secure MAC addresses not expire, they can be converted to **sticky secure MAC addresses**. They never age out and are automatically saved to the running-config like `switchport port-security mac-address sticky` followed by the MAC address. But the running-config should be saved to the startup-config to make the MAC addresses truly permanent. Sticky secure MAC address learning can be enabled with the `switchport port-security mac-address sticky` command. When this command is issued, all currently learned secure MAC addresses get converted to sticky secure MAC addresses. And vice versa, they can be converted back with the `no switchport port-security mac-address sticky` command.

Secure MAC addresses are added to the MAC address table like any other MAC address. Sticky and Static secure MAC addresses have a type of `STATIC`. Dynamically-learned secure MAC addresses have a type of `DYNAMIC`.

### ErrDisable Recovery

**ErrDisable Recovery** automatically re-enables err-disabled interfaces within a certain time interval. The default timer is 300 seconds. So, by default, every 5 minutes all err-disabled interfaces are re-enabled if err-disable recovery is enabled for the cause of the interface's disablement. To change the timer, use the command `errdisable recovery interval` followed by the number in seconds. To view the configuration, use the command `show errdisable recovery`. It lists all possible err-disable reasons and whether err-disable recovery is enabled. By default, it is disabled for all reasons. To enable err-disable recovery, enter the command `errdisable recovery cause` followed by the cause. Err-disable recovery is useless if the device that caused the interface to enter the err-disabled state is not disconnected.

### Violation Modes

There are three different violation modes that determine what the switch does if an unauthorized frame enters the interface configured with port security:&#x20;

* **Shutdown**: The switch shuts down the interface by placing it in an err-disabled state, generates a Syslog and/or SNMP message, and increments the violation counter.
* **Restrict**: The switch discards traffic from unauthorized MAC addresses but doesn't disable the interface. It also generates a Syslog and/or SNMP message each time an unauthorized MAC address is detected and increments the violation counter for each unauthorized frame.&#x20;
* **Protect**: The switch discards traffic from unauthorized MAC addresses but doesn't disable the interface. It also doesn't generate any Syslog/SNMP messages and doesn't increment the violation counter.

The command to change the violation mode is `switchport port-security violation` followed by the mode (the default is `shutdown`).

<figure><img src=".gitbook/assets/image (158).png" alt="summary" width="563"><figcaption><p>Summary</p></figcaption></figure>

{% file src=".gitbook/assets/Day 49 Flashcards - Port Security.apkg" %}

{% file src=".gitbook/assets/Day 49 Lab - Port Security.pkt" %}

{% embed url="https://youtu.be/zZwhrxKeGj8" %}
