---
description: OSPF Part 2
---

# Day 27

### Cost

OSPF's metric is known as **cost**. It is automatically calculated by dividing a **reference bandwidth** (default is 100 Mbps) value by the interface's bandwidth. All values less than 1 are converted to 1. To change the default reference bandwidth, enter the OSPF config mode and enter `auto-cost reference-bandwidth` followed by the value in Mbps. The reference bandwidth on all OSPF routers in the network should be the same.&#x20;

The OSPF cost to a destination is the total cost of the exit interfaces along the path. Loopback interfaces have a cost of 1. To manually configure the cost of an interface, enter the interface config mode and use the command `ip ospf cost` followed by the cost. Another way to change the cost is to change the interface bandwidth. It doesn't change the actual speed at which the interface operates. It is just used to calculate the OSPF cost. This method is not recommended. The command is `bandwidth` followed by the value in Kbps which is entered from the interface config mode.&#x20;

### Neighbours

The default hello timer is 10 seconds on an Ethernet connection. Hello messages are multicast to `224.0.0.5`. OSPF messages are encapsulated in an IP header with a value of 89 in the Protocol field. For OSPF routers to become neighbours, they have to go through several states.

#### Down

<figure><img src=".gitbook/assets/image (12) (1).png" alt="down state" width="563"><figcaption></figcaption></figure>

* OSPF is activated on R1's `G0/0` interface
* It sends an OSPF Hello message to `224.0.0.5`
* It doesn't know about any neighbours yet

#### &#x20;Init

<figure><img src=".gitbook/assets/image (13) (1).png" alt="init state" width="563"><figcaption></figcaption></figure>

* When R2 receives the Hello packet, it adds an entry for R1
* Hello packet is received but R2's ID is not in the Hello packet
* R1 still doesn't know about R2 yet

#### 2-way

<figure><img src=".gitbook/assets/image (14).png" alt="2-way state" width="563"><figcaption></figcaption></figure>

* Both routers receive Hello messages with their own RID included
* If both routers reach this state, it means they are ready to share LSAs to build a common LSDB
* **DR** (Designated Router) and **BDR** (Backup Designated Router) are elected at this point

#### Exstart

<figure><img src=".gitbook/assets/image (15).png" alt="exstart state" width="563"><figcaption></figcaption></figure>

* Both routers prepare to exchange information about their LSDB
* The router with the higher RID becomes the **Master** and initiates the exchange. The router with  the lower RID becomes the **Slave**
* To decide between the Master and Slave, they exchange **DBD** (Database Description) packets

#### Exchange

<figure><img src=".gitbook/assets/image (16).png" alt="exchange state" width="563"><figcaption></figcaption></figure>

* The routers exchange DBDs which contain the list of LSAs in their LSDB
* These DBDs do not contain detailed information about LSAs, just basic information
* The routers compare the information they receive with their own LSDB to determine which LSA they need to request

#### Loading

<figure><img src=".gitbook/assets/image (17).png" alt="loading state" width="563"><figcaption></figcaption></figure>

* Routers send **LSR** (Link State Request) messages to request any LSAs they don't have
* LSAs are sent in **LSU** (Link State Update) messages
* The routers then send **LSAck** (Link State Acknowledgment) messages to acknowledge that they received the LSAs

#### Full

* The routers have a full OSPF adjacency and identical LSDBs
* They continue to send Hello packets (every 10 seconds by default) to maintain the neighbour adjacency
* Every time a Hello packet is received, a **Dead** timer (40 seconds by default) is reset
* If no Hello packet is received and Dead timer reaches 0 (zero), the neighbour is removed
* The routers keep sharing LSAs as the network changes

### OSPF Message Types

There are 5 message types in OSPF:

* 1 - Hello
* 2 - DBD
* 3 - LSR
* 4 - LSU
* 5 - LSAck

### Configuration

To activate OSPF on a particular interface, enter the interface config mode and use the command `ip ospf` followed by the process ID followed by `area` and area number.

To configure all interfaces as passive by default, enter the command `passive-interface default` from the OSPF config mode. To activate the interface, just enter `no passive-interface` followed by the interface number.&#x20;

{% file src=".gitbook/assets/Day 27 Flashcards - OSPF Part 2.apkg" %}

{% file src=".gitbook/assets/Day 27 Lab - OSPF Part 2.pkt" %}

{% embed url="https://youtu.be/UEyQW-EcnY8" %}
