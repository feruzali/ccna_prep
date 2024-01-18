---
description: Day 23
---

# EtherChannel

### EtherChannel

If you connect two switches together with multiple interfaces, all except one will be disabled by the STP. It is a waste of bandwidth. **EtherChannel** groups multiple physical interfaces together to act as a single logical interface. Traffic using the EtherChannel is load balanced among the physical interfaces. EtherChannel is also known as **PortChannel**, **LAG** (Link Aggregation Group).&#x20;

<figure><img src=".gitbook/assets/image (124).png" alt="etherchannel" width="563"><figcaption></figcaption></figure>

`ASW` - **Access Layer Switch**, a switch that end hosts connect to.

`DSW` - **Distribution Layer Switch**, a switch that access switches connect to.

#### Load Balancing

EtherChannel load balances based on the **flows**. A flow is a communication between two nodes. Frames in the same flow are forwarded using the same physical interface. Depending on the switch, configuration settings for interface selection calculation can be changed based on these:

* Source MAC address
* Destionat MAC address
* Source and Destination MAC address
* Source IP address
* Destination IP address
* Source and Destination IP address

To see the current load balancing method, use `show etherchannel load-balance` command from the privileged EXEC mode. To change the config settings, enter the global config mode and use the command `port-channel load-balance` followed by the method.

#### Protocols

There are 3 methods of EtherChannel configuration: **PAgP** (Port Aggregation Protocol), **LACP** (Link Aggregation Control Protocol), and **Static**. Up to 8 interfaces can be formed into a single EtherChannel. LACP allows up to 16 but only 8 will be active, the other 8 will be in standby mode. LACP is IEEE 802.3ad standard.

#### Configuration

It is better to configure interfaces in a bunch using the `interface range` command. Enter the interface config mode and use the `channel-group` followed by virtual interface number followed by `mode` and the mode you want to use. `auto` and `desirable` modes are used for PAgP similarly to DTP. PortChannel gets created automatically. `active` and `passive` modes are used for LACP. If both ends are configured in passive mode, EtherChannel won't be formed. In all other cases, it forms an EtherChannel. `on` mode configures Static EtherChannel. It doesn't work with other modes. To manually configure the negotiation protocol, enter the `channel-protocol` command followed by the mode (`lacp`/`pagp`). To verify the EtherChannel config settings, enter `show etherchannel summary` or `show etherchannel port-channel`.

Member interfaces must have matching configurations:

* Duplex
* Speed
* Switchport mode
* VLAN settings

If an interface's configurations don't match the others, it is excluded from the EtherChannel. &#x20;

{% file src=".gitbook/assets/Day 23 Flashcards - EtherChannel.apkg" %}

{% file src=".gitbook/assets/Day 23 Lab - EtherChannel.pkt" %}

{% embed url="https://youtu.be/8gKF2fMMjA8" fullWidth="false" %}
