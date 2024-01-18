---
description: Day 2
---

# Interfaces and Cables

### Ethernet

Ethernet is a collection of network protocols/standards. A network protocol is like a common language agreed upon between networking devices used for communication.

Ethernet uses RJ-45 (RJ - Registered Jack) ports:

<figure><img src=".gitbook/assets/image (50).png" alt="RJ-45 connectors"><figcaption></figcaption></figure>

### Speed

The speed is measured in bits per second (Kbps, Mbps, Gbps, etc). A bit (binary digit) is a value represented by either 0 (zero) or 1 (one). Computers operate with bits. So, communication between devices is also done via bits.\
8 bits is called a byte. Data in the memory is measured in bytes but the speed is in bits. For example, GigaByte is 8 times larger than a Gigabit. That's why when downloading 1 Gb of data with the speed of 1 Gbps, it takes 8 seconds, not 1.

1 kilobit (Kb) = 1 000 bits\
1 megabit (Mb) = 1 000 000 bits\
1 gigabit (Gb) = 1 000 000 000 bits

### Ethernet Standards

Defined in IEEE 802.3 standards in 1983. IEEE - Institute of Electrical and Electronics Engineers. Here are Ethernet cable types and their specifications as defined in IEEE 802.3 standards:

<figure><img src=".gitbook/assets/image (110).png" alt="Ethernet standards (copper)"><figcaption></figcaption></figure>

UTP (Unshielded Twisted Pair) cables consist of 4 pairs of cables twisted together. Twisting protects against EMI (ElectroMagnetic Interference).

#### 10BASE-T and 100BASE-T

RJ-45 Ethernet connecter consists of 8 pins, perfect for UTP cables. However, 10BASE-T and 100BASE-T use only 2 pairs.&#x20;

When connecting a PC/router to a switch using Ethernet or Fast Ethernet cable, a straight-through cable is used and the pins in the NIC (Network Interface Card) are divided as follows:

<figure><img src=".gitbook/assets/image (65).png" alt="pc to switch"><figcaption></figcaption></figure>

When connecting a PC/router to a router or switch to a switch using Ethernet or Fast Ethernet cable, both devices receive and transmit in the same pair of pins, so the cable is crossed over and the cable used is called a crossover cable. The pins are divided as follows:

<figure><img src=".gitbook/assets/image (70).png" alt="switch to switch"><figcaption></figcaption></figure>

Here is the chart for different device types and pins used for transmitting and receiving data:

<figure><img src=".gitbook/assets/image (83).png" alt=""><figcaption></figcaption></figure>

Modern networking devices have a feature called Auto MDI-X which allows them to automatically adjust pins for transmitting and receiving. So, with this new feature, we don't have to worry about choosing a straight-through or crossover cable anymore.

The full-duplex transmission allows both devices to send and receive data at the same time, and no collision occurs because the wires for sending and receiving are separated. So, in the figure above, a full-duplex connection is demonstrated.&#x20;

#### 1000BASE-T and 10GBASE-T

1000BASE-T and 10GBASE-T cables use all 8 pins and each pair is bidirectional meaning that each can transmit and receive data. That's how these cables can operate at much higher speeds.

<figure><img src=".gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

### Fiber-Optic Connections

Fiber-optic uses SFP (Small Form-Factor Pluggable) Transceivers:&#x20;

<figure><img src=".gitbook/assets/image (84).png" alt="" width="375"><figcaption></figcaption></figure>

The cables used are fiber-optic cables which send light over glass fibers instead of electrical signals.&#x20;

<figure><img src=".gitbook/assets/image (109).png" alt="" width="375"><figcaption></figcaption></figure>

Fiber-optic cables use two separate cables. One is used for transmitting and the second - for receiving.&#x20;

<figure><img src=".gitbook/assets/image (71).png" alt="fiber-optic cable connection"><figcaption></figcaption></figure>

The structure of the cable is as follows:

<figure><img src=".gitbook/assets/image (75).png" alt="fiber-optic cable" width="375"><figcaption></figcaption></figure>

1. fiberglass core
2. cladding
3. protective buffer
4. outer jacket

There are two types of fiber-optic cables: single-mode and multimode.

#### Multimode fiber

<figure><img src=".gitbook/assets/image (35).png" alt="multi-mode fiber" width="563"><figcaption></figcaption></figure>

1. The core diameter is wider than single-mode fiber.
2. Allows multiple angles (modes) of light waves to enter the fiberglass core.
3. Longer cables than UTP, but shorter than single-mode fiber.
4. Cheaper than single-mode fiber due to cheaper SFP transmitters.
5. Often LED-based transmitters are used.

#### Single-mode fiber

<figure><img src=".gitbook/assets/image (47).png" alt="single-mode fiber" width="563"><figcaption></figcaption></figure>

1. Core diameter is narrower than multimode fiber.
2. Light enters at a single angle (mode).
3. Longer cables than UTP and multi-mode fiber.
4. More expensive than multi-mode fiber.
5. Laser-based transmitters are used.

### Fiber-optic cable standards

<figure><img src=".gitbook/assets/image (107).png" alt="fiber-optic cable standards"><figcaption></figcaption></figure>

{% file src=".gitbook/assets/Day 2 Flashcards - Interfaces and Cables.apkg" %}

{% file src=".gitbook/assets/Day 2 Lab - Connecting Devices.pkt" %}

{% embed url="https://youtu.be/K6Qt23sY68Y" %}
