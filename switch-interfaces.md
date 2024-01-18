---
description: Day 9
---

# Switch Interfaces

### Switch Interfaces

Cisco switch interfaces do not have `shutdown` command applied by default. So, they are in `down` state if no device is connected and automatically get `up` when connected. One more command to check switch interfaces is `show interfaces status` entered in privileged EXEC mode. The name column here displays the interface description.

<figure><img src=".gitbook/assets/image (73).png" alt="show interfaces status" width="563"><figcaption></figcaption></figure>

#### Interface Configuration

To configure the speed and duplex of an interface, you first have to enter the interface configuration mode, and enter the corresponding commands: `speed` followed by 10 or 100 measured in Mbps or auto, `duplex` followed by half/full/auto. **Half duplex** means that the device cannot send and receive data at the same time. It must wait until one operation is finished. **Full duplex** means that the device can send and receive data at the same time. In modern networks, all devices can use a full duplex.&#x20;

To configure several interfaces at the same time, you may use the command `interface range` followed by the interface numbers, e.g. `interface range f0/6 - 10`. You can even use `,` (commas) like this `interface range f0/6 - 8, f0/10 -12`.&#x20;

#### Interface Autoconfiguration

By default, interfaces automatically negotiate the best speed and duplex settings based on their capabilities. If auto-negotiation is disabled on the device connected to a switch, the switch will try to sense the speed the device operates on, if it fails, it uses the slowest one supported. And if the speed is 10 or 100 Mbps, the switch will use half duplex, if 1000 Mbps or more - full duplex.&#x20;

#### Interface Errors

To see the errors on interfaces, we enter the command `show interfaces` in privileged EXEC mode. These are the same on a router.

<figure><img src=".gitbook/assets/image (54).png" alt="interface errors" width="563"><figcaption></figcaption></figure>

* **Runts** - frames smaller than the minimum frame size (64 bytes)
* **Giants** - frames larger than the maximum frame size (1518 bytes)
* **CRC** - frames that failed the CRC check (in the Ethernet FCS trailer)
* **Frame** - frames that have an incorrect format (due to an error)
* **Input errors** - a total of various counters
* **Output errors** - frames that switch failed to send (due to an error)

### CSMA/CD

**CSMA/CD** (Carrier Sense Multiple Access with Collision Detection) describes how devices avoid collision in a half-duplex situation. Before sending frames, devices first make sure that other devices are not sending anything. And if a collision occurs, the device sends a jamming signal to inform other devices that a collision happened. Each device then will wait a random period of time before sending frames again. This kind of collision doesn't normally occur anymore since a full duplex is used. &#x20;

{% file src=".gitbook/assets/Day 9 Flashcards - Switch Interfaces.apkg" %}

{% file src=".gitbook/assets/Day 9 Lab - Interface Configuration.pkt" %}

{% embed url="https://youtu.be/rzDb5DoBKRk" %}
