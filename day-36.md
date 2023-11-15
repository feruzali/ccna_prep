---
description: CDP & LLDP
---

# Day 36

Layer 2 discovery protocols (CDP and LLDP) share information with and discover information about neighbouring devices. The shared information includes hostname, IP address, device type, etc.&#x20;

### CDP

**CDP** (Cisco Discovery Protocol) is a Cisco proprietary protocol which is enabled on all Cisco devices by default. The default version is CDPv2. CDP messages are periodically sent to multicast MAC address `0100.0ccc.cccc`. When a device receives a CDP message, it processes and discards the message without forwarding it to other devices. By default, CDP messages are sent every 60 seconds. The default hold time is 180 seconds.&#x20;

#### Verification

To see CDP configurations, enter the `show cdp` command, for CDP traffic - `show cdp traffic`, and for CDP information about each interface - `show cdp interface`. To see the CDP neighbours, enter the command `show cdp neighbors` or `show cdp neighbors detail`, for the specified neighbour - `show cdp entry` followed by the hostname.

<figure><img src=".gitbook/assets/image (3) (1) (1).png" alt="show cdp neighbors command" width="563"><figcaption></figcaption></figure>

#### Configuration

* Enable/disable CDP globally - `cdp run`/`no cdp run`.
* Enable/disable CDP on a specific interface - `cdp enable`/`no cdp enable`.
* Configure the CDP timer - `cdp timer` followed by the value in seconds.
* Configure the CDP hold time - `cdp holdtime` followed by the value in seconds.
* Enable/disable CDPv2 - `cdp advertise-v2`/`no cdp advertise-v2`.

### LLDP

**LLDP** (Link Layer Discovery Protocol) is an industry-standard protocol (IEEE 802.1ab). It is usually disabled on Cisco devices by default. A device can run CDP and LLDP at the same time. LLDP messages are multicast to MAC address `0180.c200.000e`. By default, LLDP messages are sent every 30 seconds and holdtime is 120 seconds. It also has an additional timer - reinitialization delay. When LLDP is enabled, this timer delays the actual initialization of LLDP. It is 2 seconds by default.

#### Verification

The commands and outputs are very similar to CDP.&#x20;

* For basic information - `show lldp`.
* For LLDP stats - `show lldp traffic`.
* For LLDP-enabled interfaces - `show lldp interface`.
* For LLDP neighbours - `show lldp neighbors` or `show lldp neighbors detail`, for the specified neighbour - `show lldp entry` followed by the hostname.&#x20;

<figure><img src=".gitbook/assets/image (1) (1) (1) (1) (1) (1) (1).png" alt="show lldp neighbors command" width="563"><figcaption></figcaption></figure>

#### Configuration

* Enable LLDP globally - `lldp run`.
* Enable LLDP to transmit on a specific interface - `lldp transmit`.
* Enable LLDP to receive on a specific interface - `lldp receive`.
* Configure the LLDP timer - `lldp timer` followed by the value in seconds.
* Configure the LLDP hold time - `lldp holdtime` followed by the value in seconds.
* Configure the LLDP reinit timer - `lldp reinit` followed by the value in seconds.

{% file src=".gitbook/assets/Day 36 Flashcards - CDP _ LLDP.apkg" %}

{% file src=".gitbook/assets/Day 36 Lab - CDP _ LLDP.pkt" %}

{% embed url="https://youtu.be/4s8qqL7R9W8" %}
