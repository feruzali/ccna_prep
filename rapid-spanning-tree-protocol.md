---
description: Day 22
---

# Rapid Spanning Tree Protocol

### Spanning Tree Versions

#### Spanning Tree Protocol (802.1D)&#x20;

* The original STP&#x20;
* All VLANs share one STP instance&#x20;
* Therefore, cannot load balance

#### Rapid Spanning Tree Protocol (802.1w)&#x20;

* Much faster at converging/adapting to network changes than 802.1D&#x20;
* All VLANs share one STP instance&#x20;
* Therefore, cannot load balance&#x20;

#### Multiple Spanning Tree Protocol (802.1s)&#x20;

* Uses modified RSTP mechanics&#x20;
* Can group multiple VLANs into different instances (ie. VLANs 1-5 in instance 1, VLANs 6-10 in instance 2) to perform load balancing

#### Per-VLAN Spanning Tree Plus (PVST+)

* Cisco's upgrade to 802.1D
* Each VLAN has its own STP instance&#x20;
* Can load balance by blocking different ports in each VLAN

#### Rapid Per-VLAN Spanning Tree Plus (Rapid PVST+)&#x20;

* Cisco's upgrade to 802.1w&#x20;
* Each VLAN has its own STP instance&#x20;
* Can load balance by blocking different ports in each VLAN&#x20;

The difference between PVST and PVST+ is that PVST only supports ISL trunk encapsulation (not dot1q). Standard STP BPDUs are sent to the destination MAC address of `0180.c200.0000`. But PVST BPDUs are sent to the destination MAC address of `0100.0ccc.cccd`.

### RSTP

**RSTP** is not a timer-based spanning tree algorithm like 802.1D. Therefore, RSTP offers an improvement over the 30 seconds or more that 802.1D takes to move a link to forwarding. The heart of the protocol is a new bridge-bridge handshake mechanism, which allows ports to move directly to forwarding. RSTP is compatible with classic STP. The interfaces on the RSTP-enabled switch connected to the classic STP-enabled switch will operate in classic STP mode. The **Protocol Version Identifier** is 0 (zero) for classic STP and 2 for RSTP. The same with the BPDU Type. Also, Classic STP uses only 2 bits (first and last) of BPDU flags while RSTP uses all 8. In classic STP only the root bridge originates BPDUs, and other switches just forward the BPDUs they received. In rapid STP, all switches originate and send their own BPDUs from their designated ports. All switches running RSTP send their own BPDUs every hello time (2 seconds). The max age timer is 3 BPDUs (6 seconds). It will then flush (delete) all MAC addresses learned on that interface.

#### Port Cost

Port Costs were updated in RSTP.

<figure><img src=".gitbook/assets/image (19).png" alt="rstp port cost" width="563"><figcaption></figcaption></figure>

#### Port State

RSTP combined Blocking and Disabling port states into one state (**Discarding**) and got rid of the Listening state. Here is the updated table for port states.

<figure><img src=".gitbook/assets/image (20).png" alt="rstp port states" width="563"><figcaption></figcaption></figure>

#### Port Role

Port roles for the root port and the designated port remain unchanged in RSTP. However, the non-designated port role is now split into two: **alternate** and **backup.**&#x20;

* The alternate role port role is a discarding port that receives a superior BPDU from another switch. It functions as an immediate backup for the root port.&#x20;
* The backup role port role is a discarding port that receives a superior BPDU from another interface on the same switch. This only happens when two interfaces are connected to the same collision domain (via a hub). It functions as a backup for a designated port.&#x20;

#### Link Types

There are 3 link types:

* **Edge**: a port that is connected to an end host. Directly moves to forwarding state, without negotiation.
* **Point-to-point**: a direct connection between two switches.
* **Shared**: a connection to a hub. Must operate in half-duplex.

The command to configure the link type is `spanning-tree link-type` followed by `point-to-point`/`shared`. The edge port is the same as the classic STP port with PortFast enabled.

{% file src=".gitbook/assets/Day 22 Flashcards - Rapid STP.apkg" %}

{% file src=".gitbook/assets/Day 22 Lab - Rapid STP.pkt" %}

{% embed url="https://youtu.be/YG7r4XHy2JU" %}
