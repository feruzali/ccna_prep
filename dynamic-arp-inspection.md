---
description: Day 51
---

# Dynamic ARP Inspection

**DAI** (Dynamic ARP Inspection) is a security feature of switches that is used to filter ARP messages received on untrusted ports. DAI only filters ARP messages. All ports are untrusted by default. Typically, all ports connected to other network devices should be configured as **trusted**, and interfaces connected to end hosts should remain **untrusted**.

<figure><img src=".gitbook/assets/image (160).png" alt="DAI demo" width="563"><figcaption></figcaption></figure>

### Operations

DAI inspects the `sender MAC` and `sender IP` fields of ARP messages received on untrusted ports and checks the DHCP snooping binding table. If there is a matching entry, the ARP message is forwarded normally, otherwise the ARP message is discarded. The hosts that don't use DHCP can use ARP ACLs. Those can be configured manually to map IP addresses/MAC addresses for DAI to check. DAI can also be configured to perform in-depth checks. Like DHCP snooping, DAI also supports rate limiting.

### Configuration

To configure DAI from the global config mode:

1. `ip arp inspection vlan` followed by the VLAN number - enable DAI on the specified VLAN
2. `interface` followed by the interface number - enter the interface config mode
3. `ip arp inspection trust` - make the interface trusted

To view the DAI configuration, use the command `show ip arp inspection`, for DIA settings of interfaces - `show ip arp inspection interfaces`.&#x20;

<figure><img src=".gitbook/assets/image (161).png" alt="show ip arp inspection interfaces command output" width="563"><figcaption></figcaption></figure>

### Rate-Limiting

DAI rate limiting is enabled on untrusted ports by default with a rate of 15 packets per second. It is disabled on trusted ports by default. The DAI **burst interval** allows to configure rate limiting like this - `x packets per y seconds`. So, it doesn't need to be `x packets per second` like in DHCP snooping. To configure it, use the command `ip arp inspection limit rate` followed by the number of packets and optionally you can add `burst interval` followed by the number in seconds. If you skip the optional part, the default burst interval is 1 second. If ARP messages are received faster than the specified rate, the interface is put in an err-disabled state.

### Optional Checks

To use optional checks, enter the command ip arp inspection validate followed by either `dst-mac`/`ip`/`src-mac`. If several are configured sequentially, the previous one gets overwritten. So, to enable several checks, they should be entered in a single command separated by space( ).

* `dst-mac` - enabled validation of the destination MAC address in the Ethernet header against the target MAC address in the ARP body for ARP Responses.
* `ip` - enabled validation of the ARP body for invalid and unexpected IP addresses like `0.0.0.0`, `255.255.255.255`, multicast addresses, etc.
* src-mac - enabled validation of the source MAC address in the Ethernet header against the sender MAC address in the ARP body for ARP Requests and ARP Responses.

<figure><img src=".gitbook/assets/image (159).png" alt="Summary" width="563"><figcaption><p>Summary</p></figcaption></figure>

{% file src=".gitbook/assets/Day 51 Flashcards - Dynamic ARP Inspection.apkg" %}

{% file src=".gitbook/assets/Day 51 Lab - Dynamic ARP Inspection.pkt" %}

{% embed url="https://youtu.be/HwbTKaIvL6s" %}
