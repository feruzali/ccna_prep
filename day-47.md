---
description: QoS (Part 2)
---

# Day 47

### Classification

The purpose of QoS is to give certain kinds of network traffic priority over others during congestion. Classification organizes network traffic into traffic classes. There are many methods of classifying traffic:

* ACL. Traffic which is permitted by the ACL is given a certain treatment.
* **NBAR** (Network Based Application Recognition) performs a deep packet inspection, looking beyond the Layer 3 and Layer 4 information up to Layer 7 to identify the specific kind of traffic.
* PCP and DSCP fields in the Layer 2 and Layer 3 headers can identify high-priority traffic.

PCP is also known as **CoS** (Class of Service). Its use is defined by **IEEE 802.1p**. It has 8 possible values. `0` means **best-effort** delivery. This is the regular traffic. IP phones mark call signalling traffic as PCP3 - critical applications. They mark the actual voice traffic as PCP5 - voice.

<figure><img src=".gitbook/assets/image (152).png" alt="pcp priority" width="563"><figcaption></figcaption></figure>

PCP-based priority can be used only over trunk links or access links with a voice VLAN because PCP can only be found in the dot1q header.

There are some standard markings for DSCP:

* DF (Default Forwarding) - best effort traffic. The DSCP marking is 0 (`00000`).
* EF (Expedited Forwarding) - low loss/latency/jitter traffic (usually voice). The DSCP marking is 46 (`101110`).
*   AF (Assured Traffic) - A set of 12 standard values. AF defines 4 traffic classes. All packets in a class have the same priority. Within each class, there are three levels of drop precedence. Higher drop precedence means it is more likely to be dropped during congestion. The first three bits define the class, following two - drop precedence, and the last bit is always set to 0. E.g. AF11 (DSCP 10) is written as `001010`. The formula to convert from AF value to decimal DSCP value is `8x + 2y`, `x` meaning the class, and `y` meaning the drop precedence. \


    <figure><img src=".gitbook/assets/image (146).png" alt="AF bit structure" width="563"><figcaption></figcaption></figure>
*   CS (Class Selector) - A set of 8 standard values. The first three bits represent the class, the remaining are set to 0. So, there are 8 possible values using three bits. The formula to convert from CS value to DSCP value is 8 multiplied by CS class number, e.g. CS7 is DSCP 56.\


    <figure><img src=".gitbook/assets/image (147).png" alt="CS bit structure" width="563"><figcaption></figcaption></figure>

To configure it on Cisco IOS, first create a class map using the command `class-map` followed by the name. To match the traffic, enter the command `match dscp` followed by one of the options.

RFC 4954 was developed with the help of Cisco to bring all of these values together and standardize their use. Here are some key recommendations:

* Voice traffic - EF
* Interactive video - AF4x
* Streaming video - AF3x
* High-priority data - AF2x
* Best effort - DF

### Trust boundaries

The trust boundary of a network defines where devices trust the QoS markings of received messages. If the markings are trusted, the device forwards the message without changing the markings. If not, the device changes the markings according to the configured policy. If an IP phone is connected to the switch port, it is recommended to move the trust boundary to the IP phones. This is done via configuration on the switch port connected to the IP phone.&#x20;

<figure><img src=".gitbook/assets/image (148).png" alt="trust boundary demo" width="563"><figcaption></figcaption></figure>

### Queuing and Congestion Management

An essential part of QoS is the use of multiple queues. The device can match traffic based on various factors and then place it in the appropriate queue. A scheduler is used to decide which queue traffic is forwarded from next. Prioritization allows the scheduler to give certain queues more priority than others. A common scheduling method is a weighted round-robin, meaning that packets are taken from each queue in order, cyclically and more data is taken from high-priority queues each time the scheduler reaches that queue. **CBWFQ** (Class-Based Weighted Fair Queuing) is a popular method of scheduling, using a weighted round-robin scheduler while guaranteeing each queue a certain percentage of the interface's bandwidth during congestion.

<figure><img src=".gitbook/assets/image (149).png" alt="CBWFQ demo" width="563"><figcaption></figcaption></figure>

However, it can still add delay and jitter so it is not ideal for voice and video traffic. **LLQ** (Low Latency Queuing) can solve it. It designates one or more queues as **strict priority queues**. This means that if there is traffic in the queue, the scheduler always takes the next packet from that queue until it is empty. However, it has the downside of potentially starving other queues if there is always traffic in the designated strict priority queue.

<figure><img src=".gitbook/assets/image (150).png" alt="LLQ demo" width="563"><figcaption></figcaption></figure>

### Shaping and Policing

&#x20;Traffic shaping and policing are both used to control the rate of traffic. In both cases, classification can be used to allow for different rates for different kinds of traffic. Shaping buffers traffic in a queue if the traffic rate goes over the configured rate.&#x20;

Policing drops traffic if the traffic rate goes over the configured rate. Burst traffic over the configured rate is allowed for a short period of time. This accommodates data applications which typically are bursty in nature. Instead of a constant stream of data, they send data in bursts. The amount of burst traffic allowed is also configurable.

<figure><img src=".gitbook/assets/image (151).png" alt="shaping/policing demo" width="563"><figcaption></figcaption></figure>

{% file src=".gitbook/assets/Day 47 Flashcards - QoS (Part 2).apkg" %}

{% file src=".gitbook/assets/Day 47 Lab - QoS.pkt" %}

{% embed url="https://youtu.be/63tD4t8189k" %}
