---
description: NAT (part 2)
---

# Day 45

### Dynamic NAT

In dynamic NAT, the router dynamically maps inside local addresses to inside global addresses as needed. An ACL is used to identify which traffic should be translated. A NAT pool is used to define the available inside global addresses that can be used. Although they are dynamically assigned, the mappings are still one-to-one. If there are not enough inside global addresses available, it is called **NAT pool exhaustion**.

#### Configuration

To configure dynamic NAT on Cisco IOS:

1. Define the inside and outside interfaces and from the interface config mode enter the command `ip nat` followed by `inside` - for the internal network, `outside` - for the external network.&#x20;
2. Define the traffic that should be translated by configuring an ACL. Traffic permitted by the ACL is translated. E.g. `access-list 1 permit 192.168.0.0 0.0.0.255`.
3. Define the pool of inside global IP addresses - `ip nat pool` followed by the pool name, the first and the last IP addresses in the range, and the netmask/prefix length. E.g. `ip nat pool POOL1 100.0.0.0 100.0.0.255 prefix-length 24`.
4. Configure dynamic NAT by mapping the ACL to the pool - `ip nat inside source list` followed by the ACL number, keyword `pool`, and the pool name. E.g. `ip nat inside source list 1 pool POOL1`.&#x20;

### PAT

**PAT** (Port Address Translation), aka **NAT overload**, translates both the IP address and the port number if necessary. By using a unique port number for each communication flow, a single public IP address can be used by many different internal hosts. The router keeps track of which inside local address is using which inside global address and port.&#x20;

<figure><img src=".gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1).png" alt="pat demo" width="563"><figcaption></figcaption></figure>

#### Configuration

PAT is configured the same as dynamic NAT but the keyword `overload` is added at the end of the ACL to the pool mapping command, e.g. `ip nat inside source list 1 pool POOL1 overload`.&#x20;

Another way to configure PAT is to configure the router to use its own public IP address when translating the source IP of packets. First, outside and inside interfaces must be defined. Then an ACL must be created to define the traffic that should be translated. Lastly, PAT is configured by mapping the ACL to the interface and enabling `overload`, e.g. `ip nat inside source list 1 interface g0/0 overload`.

<figure><img src=".gitbook/assets/image (2) (1) (1) (1) (1) (1) (1).png" alt="summary" width="563"><figcaption><p>Summary</p></figcaption></figure>

{% file src=".gitbook/assets/Day 45 Flashcards - NAT (Part 2).apkg" %}

{% file src=".gitbook/assets/Day 45 Lab - Dynamic NAT.pkt" %}

{% embed url="https://youtu.be/vNs1xxiwGJs" %}
