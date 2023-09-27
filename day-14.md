---
description: Subnetting (Part 2)
---

# Day 14

### Subnetting Trick

Let's take one sample network with `/26` subnet.

<figure><img src=".gitbook/assets/image (80).png" alt="/26 sample network" width="563"><figcaption></figcaption></figure>

We have to find the network address of each subnet. So, let's take a closer look at the last octet.

<figure><img src=".gitbook/assets/image (92).png" alt="last octet of /26 subnet" width="563"><figcaption></figcaption></figure>

The last bit of the network portion is `64`. This means that to find the next subnet's network address, we just need to add 64. We add 64 and we get `192.168.1.64` which is the network address of the second subnet. We add 64 again, we get `192.168.1.128` which is the network address of the third subnet, etc.

### Subnetting Practice

* The formula for the **number of subnets** is 2 to the power of `x`, where `x` is the number of borrowed bits.&#x20;
* To identify which subnet the particular host belongs to, we just write the host address in binary and change all host bits to 0 (zero) to find the network address. Finally, change it back to a dotted decimal and that's the answer.

Here is a table of different subnet sizes for Class C networks.

<figure><img src=".gitbook/assets/image (42).png" alt="subnets for class c network" width="563"><figcaption></figcaption></figure>

### Subnetting Class B

The process of subnetting Class A, Class B, and Class C networks is exactly the same. For example, to subnet a 172.16.0.0/16 network and create 80 subnets, we use the same formula:

$$
2^x
$$

where `x` is the number of borrowed bits. So, we have to borrow 7 bits since it creates 128 subnets. And the subnet mask is `/23`. The first subnets look like this.

<figure><img src=".gitbook/assets/image (87).png" alt="/23 subnets" width="563"><figcaption></figcaption></figure>

Here is a table of different subnet sizes for Class B networks.

<figure><img src=".gitbook/assets/image (66).png" alt="subnets for class b network" width="563"><figcaption></figcaption></figure>

It is not necessary to memorize everything, it's enough just to understand the pattern. For each borrowed bit, the number of subnets doubles. For each host bit, the number of addresses in each subnet doubles but we have to subtract 2 to identify the number of usable host addresses.
