---
description: DHCP Snooping
---

# Day 50

DHCP Snooping is a security feature of switches that is used to filter DHCP messages received on untrusted ports. All ports are untrusted by default.&#x20;

<figure><img src=".gitbook/assets/image (6) (1) (1) (1) (1) (1).png" alt="DHCP Snooping demo" width="563"><figcaption></figcaption></figure>

DHCP Snooping only filters DHCP messages, non-DHCP messages aren't affected. When it filters messages, it differentiates between DHCP Server messages and DHCP Client messages.&#x20;

* `CHADDR` (Client Hardware Address) field in the DHCP message indicates the MAC address of the client
* `NAK` - message sent by DHCP Server to decline a client's REQUEST
* `DECLINE` - message used by DHCP Client to decline the IP address offered by a DHCP Server

### Operations

If a DHCP message is received on a trusted port, it is forwarded as normal without any inspection. If a DHCP message is received on an untrusted port, it is inspected and if it is a DHCP Server message, it gets discarded, otherwise:

* `DISCOVER`/`REQUEST` messages: if the frame's source MAC address and the DHCP message's CHADDR fields match, it is forwarded, otherwise - discarded.
* `RELEASE`/`DECLINE` messages: if the packet's source IP address and the receiving interface match the entry in the **DHCP Snooping Binding Table**, it is forwarded, otherwise - discarded.

When a client successfully leases an IP address from a server, a new entry in the DHCP Snooping Binding Table is created. To view it, use the command `show ip dhcp snooping binding`.

### Configuration

To configure DHCP snooping from the global config mode:

1. `ip dhcp snooping` - enable DHCP Snooping globally on a switch
2. `ip dhcp snooping vlan` followed by the VLAN number - enable DHCP Snooping on a VLAN
3. `no ip dhcp snooping information option` - Option 82 (aka DHCP relay agent information option). It provides additional information about which DHCP relay agent received the client's message, on which interface, VLAN, etc. It is used by DHCP relay agents. When DHCP Snooping is enabled, by default Cisco switches add Option 82 to DHCP messages they receive from clients, even if the switch is not a DHCP relay agent. By default, Cisco switches drop DHCP messages with Option 82 that are received on an untrusted port. That's why Option 82 needs to be disabled.
4. `interface` followed by the interface number - enter the interface config mode
5. `ip dhcp snooping trust` - make the interface trusted

### Rate-Limiting

DHCP snooping can limit the rate at which DHCP messages are allowed to enter an interface. If the rate of DHCP messages crosses the limit, the interface is put on err-disabled mode. The interface can then be re-enabled manually or automatically with errdisable recovery. To configure the rate limit on an interface, use the command `ip dhcp snooping limit rate` followed by the number (of messages per second).

<figure><img src=".gitbook/assets/image (1) (1) (1) (1) (1) (1) (1).png" alt="Summary" width="563"><figcaption><p>Summary</p></figcaption></figure>

{% file src=".gitbook/assets/Day 50 Flashcards - DHCP Snooping.apkg" %}

{% file src=".gitbook/assets/Day 50 Lab - DHCP Snooping.pkt" %}

{% embed url="https://youtu.be/YMom_e545H4" %}
