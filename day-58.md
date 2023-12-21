---
description: Wireless Configuration
---

# Day 58

Here is the network topology which will be used to configure the devices:

<figure><img src=".gitbook/assets/image (1) (1) (1).png" alt="network topology" width="563"><figcaption></figcaption></figure>

The WLC connects to the switch via a LAG (Link Aggregation Group). WLCs only support static LAG, no PAgP or LACP.

### Switch Configuration

<figure><img src=".gitbook/assets/image (2) (1) (1).png" alt="switch config" width="563"><figcaption></figcaption></figure>

1. The VLANs are configured
2. Access ports are configured with PortFast enabled. WLC's GUI can be only accessed via the network using HTTP/HTTPS.
3. Connection to WLC is statically configured.
4.  The PortChannel interface is configured. Allowed VLANs are specified.\


    <figure><img src=".gitbook/assets/image (3) (1) (1).png" alt="switch config" width="563"><figcaption></figcaption></figure>
5. SVIs are configured for each VLAN.
6. DHCP pools are configured for each VLAN. Option 43 can be used to tell the APs the IP address of their WLC. This is not necessary in our situation since the APs and WLC are in the same subnet. The WLC can hear the APs broadcast CAPWAP discovery messages.
7. NTP server is specified.

### WLC Setup

<figure><img src=".gitbook/assets/image (4) (1).png" alt="WLC init" width="563"><figcaption></figcaption></figure>

Autoinstall uses a TFTP server to get the configuration, it is not needed in this case. So, just pressing enter skips it. Then, WLC username and password configuration are done. Then, further network configuration is done.

<figure><img src=".gitbook/assets/image (5) (1).png" alt="WLC init" width="563"><figcaption></figcaption></figure>

**Virtual Gateway IP** is used when the WLC is communicating directly with wireless clients (ie relaying DHCP requests). **Multicast IP** is used when forwarding traffic to its APs. **Mobility/RF Group Name** is used when you have multiple WLCs and you want them to work together. We will change the WLAN security policy to PSK so we don't need to configure a RADIUS server. You have to be careful when entering a Country Code because if the regulatory domain of the country specified in the WLC configuration doesn't match the regulatory domain of the AP, the AP won't be able to join the WLC. The regulatory domain of the device is specified on the back side of the device.

<figure><img src=".gitbook/assets/image (6) (1).png" alt="WLC init" width="563"><figcaption></figcaption></figure>

Finally, the wireless network protocols are enabled and the NTP server is specified if exists.

### WLC GUI

To get access to the WLC GUI, the PC should be connected to the switch. From the PC, open a web browser and enter the internal IP address of the WLC. The warning might be shown, click the  `Advanced` button, then `Proceed`. After you enter the GUI, click the `Login` button and enter the username and password configured on the WLC.&#x20;

WLC ports are the physical ports that cables connect to. WLCs have different kinds of ports:

* **Service port** - a dedicated management port. Used for out-of-band management. Must connect to a switch access port because it only supports one VLAN. This port can be used to connect to the device while it's booting, perform system recovery, etc.
* **Distribution system port** - standard network ports that connect to the distribution system (wired network) and are used for data traffic. These ports usually connect to switch trunk ports and if multiple distribution ports are used, they can form a LAG.
* **Console port** - standard console port, either RJ45 or USB.
* **Redundancy port** - used to connect to another WLC to form a **HA** (high availability) pair.

WLC interfaces are the logical interfaces within the WLC (ie SVIs on a switch). WLCs have different kinds of interfaces:

* **Management interface** - used for management traffic such as Telnet, SSH, HTTP/HTTPS, RADIUS, authentication, etc. CAPWAP tunnels are also formed to/from this interface.
* **Redundancy management interface** - when two WLCs are connected, one is active, another one is a standby. This interface can be used to connect to and manage the standby WLC.
* **Virtual interface** - This interface is used when communicating with wireless clients to relay DHCP requests, perform client web authentication, etc.
* **Service port interface** - if the service port is used, this interface is bound to it and is used for out-of-band management.
* **Dynamic interface** -  used to map a WLAN to a VLAN. Traffic from the internal WLAN is sent to the wired network from the WLC's internal dynamic interface.

### WLC Configuration

To configure the interface, click `Controller`, then `Interfaces`. Create a new Internal interface with VLAN ID 100 using the `New` button. Specify an IP address, netmask, and gateway address. That's it for creating an interface. Do the same for the Guest interface.

To configure the WLANs, go the the `WLANs` tab.

<figure><img src=".gitbook/assets/image (162).png" alt="WLC WLANs config panel" width="563"><figcaption></figcaption></figure>

The WLAN Internal is listed and it is mapped to the management interface. It should be changed to Internal. To use the PSK instead of 802.1X, go to the `Security` tab and in the `Authentication Key Management` section, select PSK instead of 802.1X. In PSK format, the password can be specified. Using ASCII, enter the password and apply the changes. Then, a Guest WLAN needs to be created and configured the same way.

{% file src=".gitbook/assets/Day 58 Flashcards - Wireless Configuration.apkg" %}

{% file src=".gitbook/assets/Day 58 Lab - Wireless LANs.pkt" %}

{% embed url="https://youtu.be/Il8ev78fcqw" %}
