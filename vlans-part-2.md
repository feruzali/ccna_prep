---
description: Day 17
---

# VLANs (Part 2)

### Trunk Ports

In a small network with few VLANs, it is possible to use a separate interface for each VLAN when connecting switches to switches and switches to routers. However, when the number of VLANs increases, it is not viable. So we can use **trunk ports**. Unlike access ports, trunk ports carry traffic from multiple VLANs on a single interface.&#x20;

<figure><img src=".gitbook/assets/image (119).png" alt="network topology" width="563"><figcaption></figcaption></figure>

For example, for this network topology, we can replace some connections with trunk ports.

<figure><img src=".gitbook/assets/image (120).png" alt="topology with trunk ports" width="563"><figcaption></figcaption></figure>

Here we replaced switch-to-switch and router-to-switch connections. And to identify which VLAN the frame belongs to, switches will tag all frames that they send over a trunk link. Trunk ports are also called **tagged ports**.

#### VLAN Tagging

There are two main Trunking Protocols: **ISL** (Inter-Switch Link) and IEEE 802.1Q. Modern Cisco equipment doesn't support ISL, so it will probably never be used.

### 802.1Q

**802.1Q** field is inserted into the frame header between the **Source** and **Type/Length** fields.

<figure><img src=".gitbook/assets/image (117).png" alt="frame header w/ 802.1q" width="563"><figcaption></figcaption></figure>

The tag is 4 bytes in length. It consists of two main fields:

* **TPID** (Tag Protocol Identifier)
* **TCI** (Tag Control Information)

TCI consists of three sub-fields:

* **PCP** (Priority Code Point)
* **DEI** (Drop Eligible Indicator)
* **VID** (VLAN ID)

#### TPID

TPID is 16 bits in length.  Always set to a hexadecimal value of `8100`. This indicates that the frame is 802.1Q-tagged.

#### PCP

PCP is 3 bits in length and used for **CoS** (Class of Service) which prioritizes important traffic in congested networks.

#### DEI

DEI is just a single bit in length and is used to indicate the frames that can be dropped if the network gets congested.

#### VID

VID is 12 bits in length. It is the field which actually identifies the VLAN the frame belongs to. The range is 0-4095. But VLANs `0` and `4095` are reserved and cannot be used.

Here is the 802.1Q tag format:

<figure><img src=".gitbook/assets/image (118).png" alt="802.1q tag format" width="563"><figcaption></figcaption></figure>

The range of VLANs is divided into two sections:

* Normal VLANs (1-1005)
* Extended VLANs (1006-4094)

### Native VLAN

The **native VLAN** is VLAN 1 by default on all trunk ports. But this can be manually configured as well. The switch doesn't add an 802.1Q tag to frames in the native VLAN. When a switch receives an untagged frame on a trunk port, it assumes the frame belongs to the native VLAN. For security purposes, it's best to change the native VLAN to an unused VLAN. The command to change the VLAN is `switchport trunk native vlan` followed by the VLAN number.

### Trunk Configuration

To assign the interface to VLAN, enter the interface configuration mode. Use the `switchport mode trunk` command to set the interface as a **trunk port**. But first, you need to set the encapsulation to 802.1Q or ISL. The command to do so is `switchport trunk encapsulation` followed by either `dot1q` or `isl`. On switches that support only 802.1Q, this is not necessary. After you set the encapsulation mode, you can then configure the interface as a trunk. To view the trunk configuration, enter the `show interfaces trunk` command from the privileged EXEC mode.

#### Modifying allowed VLANs

The command to modify allowed VLANs is `switchport trunk allowed vlan` followed by options:&#x20;

* &#x20;You just enter the VLAN IDs. It allows you to configure the list of VLANs allowed.&#x20;
* `add` - adds specified VLANs to the currently existing list
* `all` - allows all VLANs on the trunk&#x20;
* `except` - allows all VLANs except ones specified
* `none` - disallows all VLANs on the trunk
* `remove` - removes a specified VLAN from the list

### ROAS

**ROAS** (Router on a Stick) is used to route between multiple VLANs using a single interface on the router and switch. No additional configuration on a switch is needed, just make sure that the interface is configured as a trunk. To configure a ROAS on a router, first, enter the subinterface configuration mode. To do so, enter `interface` followed by the interface and subinterface numbers. E.g. `interface g0/0.10`. The subinterface number doesn't have to match the VLAN number. However, it is highly recommended that they match. The next command is `encapsulation dot1q` followed by the VLAN number. Finally, simply assign an IP address to the subinterface.

{% file src=".gitbook/assets/Day 17 Flashcards - VLANs Part 2.apkg" %}

{% file src=".gitbook/assets/Day 17 Lab - VLANs Part 2.pkt" %}

{% embed url="https://youtu.be/iRkFE_lpYgc" %}
