---
description: Day 24
---

# Dynamic Routing

A **network route** is a route to a network/subnet (mask length < `/32`). A **host route** is a route to a specific host (`/32` mask).&#x20;

### Dynamic Routing

Instead of configuring static routes on each router, we can enable **dynamic routing protocol** so that routers advertise connected networks to their neighbours. Routers also advertise information about the routes they know from other routers. If some connection fails, routers will adapt their routing tables accordingly. But if static routing was used, other routers would be unaware of the failure.

Routers form **adjacencies**/**neighbour relationships**/**neighborships** with adjacent routers to exchange the routing information. If multiple routes to a destination are learned, the router determines which route is superior and adds it to the routing table. It uses the **metric** of the route to determine which route is superior (the one with the lower metric is superior).

#### Types

There are two main categories:

* **IGP** (Interior Gateway Protocol) is used to share routes within a single AS (autonomous system) which is a single organization
* **EGP** (Exterior Gateway Protocol) is used to share routes between different AS

In the example below, IGP is marked as <mark style="color:red;">red</mark> and EGP - as <mark style="color:purple;">purple</mark>.

<figure><img src=".gitbook/assets/image (125).png" alt="igp and egp example" width="563"><figcaption></figcaption></figure>

#### Algorithms

There is only one type of EGP algorithm - Path Vector and only one EGP used in modern networks - **BGP** (Border Gateway Protocol).

IGP has two algorithm types:

* Distance Vector - **RIP** (Routing Information Protocol) and **EIGRP** (Enhanced Interior Gateway Routing Protocol)
* Link State - **OSPF** (Open Shortest Path First) and **IS-IS** (Intermediate System to Intermediate System)

**Distance Vector** protocols were invented before Link State protocols and called so because the routers only learn the distance (metric) and vector (direction) of each route. The routers don't know about the network beyond their neighbours. Distance Vector protocols operate by sending information about their known destination networks and the metric to reach them. These are only shared with their directly connected neighbours. This method is also called **routing by rumor**.

When using a **Link State** routing protocol, every router creates a **connectivity map** of the network. To allow this, each router advertises information about its interfaces (connected networks) to its neighbours. These advertisements are passed along to other routers until all routers in the network develop the same map of the network. Each router independently uses this map to calculate the best routes to each destination. Link state protocols use more resources (CPU) on the router because more information is shared. However, Link State protocols are faster in reacting to changes in the network than Distance Vector protocols.

### Metrics

A router's routing table contains the best route to each destination network it knows about.  It uses the **metric** value of the routes to determine which is best. Each routing protocol uses a different metric. If a router learns two or more routes via the same routing protocol to the same destination with the same metric, both are added to the routing table and traffic is load-balanced. It is called **ECMP** (Equal Cost Multi-Path). Static routes don't use the concept of metric.

* **RIP** uses metrics based on hop count. The total metric is the total number of hops to the destination.
* **EIGRP** uses metrics based on bandwidth and delay. By default, the bandwidth of the slowest link in the route and the total delay of all links in the route are used.
* **OSPF**'s metrics are based on cost. The total metric is the total cost of each link in the route.
* **IS-IS**'s metrics are also based on cost but the cost of each link is not calculated automatically, by default. All links have a cost of 10 by default.&#x20;

### Administrative Distance

In most cases, companies use only one IGP. However, sometimes there is a need to compare different routing protocols when there are two in use. A metric is used to compare the routes learned via the same routing protocol. But **AD** (Administrative Distance) is used to compare the routes learned via different routing protocols and determine which one is better. A lower AD is preferred. Here is a chart summarizing ADs of different routing protocols on Cisco devices.

<figure><img src=".gitbook/assets/image (126).png" alt="routing protocol ADs" width="563"><figcaption></figcaption></figure>

To change the AD of a static route, just enter the number at the end of the `ip route` command while configuring a static route. By changing the AD of a static route, you can make it less preferred than routes learned via dynamic routing protocols. This is called a **floating static route**.

{% file src=".gitbook/assets/Day 24 Flashcards - Dynamic Routing.apkg" %}

{% file src=".gitbook/assets/Day 24 Lab - Floating Static Routes.pkt" %}

{% embed url="https://youtu.be/KuKC0G3LZc8" %}
