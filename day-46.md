---
description: QoS (Part 1)
---

# Day 46

### IP Phones

Traditional phones operate over the **PSTN** (Public Switched Telephone Network), aka **POTS** (Plain Old Telephone Service). IP phones use **VoIP** (Voice over IP) technologies to enable phone calls over an IP network. IP phones are connected to a switch just like any other end host. IP phones have an internal 3-port switch: **uplink** to the external switch, **downlink** to the PC, and the one that connects internally to the phone itself. This allows the PC and the IP phone to share a single switch port. Traffic from the PC passes through the IP phone to the switch.

<figure><img src=".gitbook/assets/image (142).png" alt="ip phone 3-port switch" width="563"><figcaption></figcaption></figure>

It is recommended to separate voice traffic and data traffic by placing them in separate VLANs. This can be accomplished using a voice VLAN. Traffic from the PC is untagged but the traffic from the IP phone is tagged with a VLAN ID.

To configure the voice VLAN, first configure the interface as an access port and assign a VLAN. Then, enter the command `switchport voice vlan` followed by a new VLAN number for voice VLAN from the interface config mode.

### PoE

**PoE** (Power over Ethernet) allows **PSE** (Power Sourcing Equipment) to provide power to **PD**s (Powered Devices) over an Ethernet cable. Usually, the PSE is a switch and PDs are IP phones, IP cameras, etc. The PSE receives AC power from the outlet, converts it to DC power, and supplies the DC power to the PDs.

<figure><img src=".gitbook/assets/image (143).png" alt="poe demo" width="563"><figcaption></figcaption></figure>

PoE has a process to determine if a connected device needs power and how much power it needs. When a device is connected to a PoE-enabled port, the PSE sends low-power signals, monitors the response, and determines how much power the PD needs. If the device needs power, the PSE supplies the power to allow the PD to boot. The PSE continues to monitor the PD and supply the required amount of power. **Power policing** can be configured to prevent a PD from taking too much power. The commands `power inline police` / `power inline police action err-disable` configure power policing with the default settings - disable the port and send a Syslog message if a PD draws too much power. The command `power inline police action log` doesn't shut down the interface if the PD draws too much power. It restarts the interface and sends a Syslog message. The commands are entered from the interface config mode.

<figure><img src=".gitbook/assets/image (144).png" alt="poe standards" width="563"><figcaption></figcaption></figure>

### QoS

**QoS** (Quality of Service) is a set of tools used by network devices to apply different treatments to different packets. QoS is used to manage the following characteristics of network traffic:

* **Bandwidth** - the overall capacity of the link, measured in bits per second. QoS tools allow to reserve a certain amount of a link's bandwidth for specific kinds of traffic.
* **Delay** - the amount of time it takes traffic to go from source to destination.
* **Jitter** - the variation in one-way delay between packets sent by the same application. IP phones have a jitter buffer to provide a fixed delay to audio packets.
* **Loss** - the percentage of packets sent that don't reach their destination. It can be caused by faulty cables or when a device's packet queues get full and the device starts discarding packets.

The standards recommended for acceptable interactive audio quality are:

* one-way delay: 150ms or less
* jitter: 30ms or less
* loss: 1% or less

If a network device receives messages faster than it can forward them out, the messages are placed in a queue. By default, queued messages are forwarded in a FIFO (First In First Out) manner. If the queue is full, new packets are dropped. This is called **tail drop**. Tail drop can lead to **TCP global synchronization**.

<figure><img src=".gitbook/assets/image (145).png" alt="tcp global sync" width="563"><figcaption></figcaption></figure>

A solution to prevent tail drop and TCP global synchronization is **RED** (Random Early Detection). When the amount of traffic in the queue reaches a certain threshold, the device starts randomly dropping packets from select TCP flows. Those TCP flows that drop packets reduce the rate at which the traffic is sent, but global TCP synchronization is avoided. In standard RED, all kinds of traffic are treated the same. An improved version, **WRED** (Weighted Random Early Detection) allows to control which packets are dropped depending on the traffic class.

{% file src=".gitbook/assets/Day 46 Flashcards - QoS (Part 1).apkg" %}

{% file src=".gitbook/assets/Day 46 Lab - Voice VLANs.pkt" %}

{% embed url="https://youtu.be/kGX76QNIjsE" %}
