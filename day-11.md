---
description: Routing Fundamentals
---

# Day 11

### Routing

**Routing** is the process that routers use to determine the path that IP packets take over a network to reach their destination. Routers store routes to all of their known destinations in a **routing table**. When routers receive a packet, they look in the routing table to find the best path to forward the packet. Each **route** is an instruction which tells a router where to send the packet. Two methods routers use to learn routes:

* **Static routing**: a network engineer manually configures routes on the router
* **Dynamic routing**: routers use dynamic routing protocols to share routing information with each other automatically and build their routing tables&#x20;

To view the routing table on a router, just enter `show ip route` from the privileged EXEC mode.

<figure><img src=".gitbook/assets/image (67).png" alt="routing table"><figcaption></figcaption></figure>

The `Codes` legend in the output lists the different protocols which routers can use to learn routes as well as the codes which represent them in the routing table. Here are a few of them:

* **L** - **local**.  A route to the actual IP address configured on the interface (with a `/32` netmask). An IP address of the interface on the router itself. If a router receives a packet destined for this IP address, it doesn't forward it anywhere.
* **C** - **connected**. A route to the network to which the interface is connected (with the actual netmask configured on the interface). It provides a route to all hosts in that network. If a router receives a packet with a destination in the range of that network, it forwards the packet via that interface.

These routes (2 routes per interface) are automatically added to the routing table when enabling the interface on the router after configuring an IP address.&#x20;

When choosing a route, if a packet is matched by two rules, a router chooses the **most specific** one. E.g. the route  `192.168.0.1/24` includes 256 different IP addresses but `192.168.1.1/32` includes only one. So, the second one is more specific. The most specific matching route means the matching route with the longest prefix length.&#x20;

Unlike switches, if routers don't have a route to the packet's destination, they just drop it.&#x20;

### Default Gateway

Hosts must send packets to their **default gateway** to be able to communicate outside of their local network. The default gateway is a router. The default gateway configuration is also called a **default route**. Basically, it is a route to `0.0.0.0/0` - includes all addresses from `0.0.0.0` to `255.255.255.255`.  It is the least specific route possible. If a router doesn't have any more specific routes that match a packet's destination IP address, the router will forward the packet using the default route. A default route is often used to direct traffic to the Internet. To configure a default route, the command `ip route 0.0.0.0 0.0.0.0` followed by the default gateway IP address is entered from the global configuration mode. The default route is marked `S*` in a routing table. It is possible to have more than one default route.

When an end host wants to send a message outside of its local network, the Layer 3 destination address (IP address) is the final destination's address. However, the Layer 2 destination address (MAC address) is the router's address because a packet first should be forwarded to the router.&#x20;

### Sample Topology

<figure><img src=".gitbook/assets/image (94).png" alt="sample topology"><figcaption></figcaption></figure>

If PC1 wants to send a message to PC4, the destination IP address is PC4's address but the destination MAC address is R1's G0/2 interface's MAC address. When R1 receives a frame, it de-encapsulates it and looks at the inside packet. It then checks the routing table for the most specific matching route. But it drops the packet since it doesn't know the route to PC4.  We have to ensure two-way reachability for PC1 and PC4 to be able to communicate. So, each router in the path should know the routes to `192.168.1.0/24` and `192.168.4.0/24`. They have to be manually configured.

#### Static Routes Configuration

<figure><img src=".gitbook/assets/image (52).png" alt="static routes" width="563"><figcaption></figcaption></figure>

Let's take a path via the R3 router and configure the routes as shown in the table above. The command for static route configuration is `ip route` followed by IP address, netmask, and next hop address. E.g. `ip route 192.168.4.0 255.255.255.0 192.168.13.3`. The command is entered from the global configuration mode. When configuring a static route instead of entering the next hop address, you can enter an exit interface. That means you specify which interface the router should send the packet out of rather than telling it the actual IP address of the next hop. E.g. `ip route 192.168.4.0 255.255.255.0 g0/0`. Also, you can specify both. E.g. `ip route 192.168.4.0 255.255.255.0 g0/0 192.168.13.3`. Static routes in which you specify only the exit interface rely on a feature called **Proxy ARP** to function and are displayed as `directly connected` in a routing table.

Finally, after we configured all the routes, we can check the reachability by using the `ping` command. If the pings are successful, that means there is two-way reachability.&#x20;

{% file src=".gitbook/assets/Day 11 (part 1) Flashcards - Routing Fundamentals.apkg" %}

{% file src=".gitbook/assets/Day 11 (part 2) Flashcards - Static Routing.apkg" %}

{% file src=".gitbook/assets/Day 11 Lab - Configuring Static Routes.pkt" %}

{% file src=".gitbook/assets/Day 11 Lab - Troubleshooting Static Routes.pkt" %}

{% embed url="https://youtu.be/XHxOtIav2k8" %}

{% embed url="https://youtu.be/3z8YGEVFTiA" %}
