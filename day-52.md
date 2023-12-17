---
description: LAN Architectures
---

# Day 52

### Network Topology Types

* **Star** - when several devices all connect to one central device. It is often called **star topology**.
* **Full Mesh** - when all devices are connected to each other.
* **Partial Mesh** - when some devices are connected to each other but not all.

<figure><img src=".gitbook/assets/image (9).png" alt="types of network topology" width="563"><figcaption></figcaption></figure>

### Two-Tier LAN

The two-tier LAN (aka **Collapsed Core**) design consists of two hierarchical layers: **Access Layer** and **Distribution Layer** (aka **Aggregation Layer**).

The functions of the Access Layer:

* connects to end hosts (PCs, printers, cameras, etc.)
* typically Access Layer switches have lots of ports for end hosts to connect to
* QoS marking is typically done here
* security services like port security, DAI, etc. are typically performed here
* switchports might be PoE-enabled for wireless APs, IP phones, etc.

The functions of the Distribution Layer:

* aggregates connections from the Access Layer Switches
* typically is the border between Layer 2 and Layer 3
* connects to services (Internet, WAN, etc.)

<figure><img src=".gitbook/assets/image (1) (1).png" alt="2-tier LAN example" width="563"><figcaption></figcaption></figure>

### Three-Tier LAN

In large networks with many Distribution Layer switches, the number of connections required between Distribution Layer switches grows rapidly. To help scale LAN networks, a Core Layer can be added. It is recommended to add a Core Layer if there are more than three Distribution Layers in a single location.

The function of the Core Layer:

* connects Distribution Layers in large LAN networks
* the focus is speed (**fast transport**)
* CPU-intensive operations like security, QoS marking/classification, etc. should be avoided at this Layer
* connections are all Layer 3, no spanning tree
* should maintain connectivity throughout the LAN even if devices fail

<figure><img src=".gitbook/assets/image (2) (1).png" alt="3-tier LAN example" width="563"><figcaption></figcaption></figure>

### Spine-Leaf Architecture

**Data centers** are dedicated spaces/buildings used to store computer systems like servers and network devices. Traditional data center designs used a three-tier architecture. This worked well when most of the traffic in data centers was North-South. With the precedence of virtual servers, applications are often deployed in a distributed manner (across multiple physical servers) which increases the amount of East-West traffic.

<figure><img src=".gitbook/assets/image (3) (1).png" alt="north-south, east-west traffic " width="563"><figcaption></figcaption></figure>

The traditional three-tier architecture led to bottlenecks in bandwidth and variability in server-to-server latency. To solve this, Spine-Leaf architecture (aka Clos architecture) was developed.&#x20;

The rules of Spine-Leaf architecture:

* Every Leaf switch is connected to every Spine switch.
* Leaf switches do not connect to other Leaf switches.
* Spine switches do not connect to other Spine switches.
* End hosts only connect to Leaf switches.

The path of traffic is randomly chosen to balance the traffic load among the Spine switches. Each server is separated by the same number of hops (except those connected to the same Leaf). It provides consistent latency for East-West traffic.

<figure><img src=".gitbook/assets/image (4) (1).png" alt="Spine-Leaf architecture demo" width="563"><figcaption></figcaption></figure>

### SOHO

**SOHO** (Small Office/Home Office) is the office of a small company or a home with few devices. SOHO networks don't have complex needs, so all networking functions are typically provided by a single device, often called a **home router** or **wireless router**. This one device can serve as a router, switch, firewall, wireless access point, and modem at the same time.

<figure><img src=".gitbook/assets/image (5) (1).png" alt="SOHO example" width="563"><figcaption></figcaption></figure>

{% file src=".gitbook/assets/Day 52  Flashcards - LAN Architectures.apkg" %}

{% file src=".gitbook/assets/Day 52 Lab - STP _ HSRP Synchronization.pkt" %}

{% embed url="https://youtu.be/BgIEhyoETgU" %}
