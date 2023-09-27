---
description: DTP/VTP
---

# Day 19

### DTP

**DTP** (Dynamic Trunking Protocol) is a Cisco proprietary protocol that allows Cisco switches to dynamically determine their interface status (`access` or `trunk`) without manual configuration. It is enabled by default on all Cisco switches. But for security purposes, manual configuration is recommended and DTP should be disabled on all switchports. DTP will not form a trunk with a router, PC, etc. The switchport will be in access mode.

#### Modes

A switchport in **dynamic desirable** mode will actively try to form a trunk with other Cisco switches. It will form a trunk if connected to another switchport in the following modes:

* `switchport mode trunk`
* `switchport mode dynamic desirable`
* `switchport mode dynamic auto`

To check the interface status, enter `show interfaces` followed by the interface name and `switchport` from the privileged EXEC mode.

A switchport in **dynamic auto** mode will not actively try to form a trunk with other Cisco switches, however, it will form a trunk if the switch it is connected to is actively trying to form a trunk. It will form a trunk with a switchport in the following modes:

* `switchport mode trunk`
* `switchport mode dynamic desirable`

Here is a chart summarizing the operational mode given two administrative modes:

<figure><img src=".gitbook/assets/image (121).png" alt="two modes - result" width="563"><figcaption></figcaption></figure>

#### Configuration

To configure DTP, enter `switchport mode dynamic` followed by `auto` or `desirable` from the interface config mode. To disable DTP on an interface, enter `switchport nonegotiate`. Configuring an access port also disables DTP on an interface. On older switches **dynamic desirable** is the default mode while in newer switches the default mode is **dynamic auto**.

#### Trunking Encapsulation&#x20;

Switches that support both **802.1Q** and **ISL** trunk encapsulations can use DTP to negotiate the encapsulation they will use. The negotiation is enabled by default and ISL is favored over 802.1Q. DTP frames are sent in VLAN1 when using ISL, or in the native VLAN when using 802.1Q.

### VTP

**VTP** (VLAN Trunking Protocol) allows configuring VLANs on a central VTP server switch, and other switches (VTP clients) will synchronize their VLAN database with the server. It is rarely used, and not recommended to use. There are three versions (1, 2, 3) and three modes (server, client, transparent) of VTP. Cisco switches operate in server mode by default.&#x20;

#### Modes

VTP **Servers** can add/modify/delete VLANs. They store the VLAN database in NVRAM. They increase the **revision number** each time a VLAN is added/modified/deleted. A revision number is used to determine the newest version of the VLAN database. VTP servers also synchronize with each other.

VTP **Clients** cannot add/modify/delete VLANs. They don't store the VLAN database in NVRAM (in VTPv3 they do). They synchronize with the server with the highest revision number. VTP advertisements are sent only via trunk ports on the same VTP domain.

Switches in VTP **Transparent** mode don't participate in the VTP domain. They can add/modify/delete VLANs. They maintain their own VLAN database in NVRAM but they don't advertise it to other switches. However, they forward VTP advertisements that are in the same domain.

#### Configuration

To check VTP status, enter `show vtp status` from privileged EXEC mode. VTPv1 and VTPv2 don't support the extended VLAN range (1006-4094). To change the VTP domain, enter `vtp domain` followed by the name from the global config mode. The command to change the VTP mode is `vtp mode` followed by the mode. Changing the VTP domain to an unused domain or VTP mode to transparent resets the revision number to 0 (zero). To change the VTP version, enter `vtp version` followed by the version number. Changing the VTP version increases the revision number. The major difference between VTPv1 and VTPv2 is that VTPv2 supports Token Ring VLANs.

{% file src=".gitbook/assets/Day 19 Flashcards - DTP_VTP.apkg" %}

{% file src=".gitbook/assets/Day 19 Lab - DTP_VTP.pkt" %}

{% embed url="https://youtu.be/ngTns2vF_44" %}
