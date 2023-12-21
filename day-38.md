---
description: DNS
---

# Day 38

### DNS

**DNS** (Domain Name System) is used to resolve human-readable names to IP addresses. Devices do not use names, they use addresses. When you type the name of a website into your browser, your device asks a DNS server for the IP address of the website.

<figure><img src=".gitbook/assets/image (4) (1) (1) (1) (1) (1) (1).png" alt="dns demo" width="563"><figcaption></figcaption></figure>

The hosts can automatically learn the address of the DNS server via **DHCP**. To see the basic IP configuration info on Windows, enter the command `ipconfig` from the command prompt. For more detailed output, use `ipconfig /all`. To ask a DNS server for an IP address of the specific website, use the command `nslookup` on Windows. To ping a device with a specific number of pings on Windows, use the command `ping` followed by an IP address, option `-n`, and the number of pings to send.

<figure><img src=".gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt="nslookup demo" width="563"><figcaption></figcaption></figure>

DNS `A` records are used to map names to IPv4 addresses, and `AAAA` records - for IPv6. DNS uses both TCP and UDP. Standard DNS messages use UDP. TCP is used for DNS messages greater than 512 bytes. The port used is 53.

#### Cache

Devices save the DNS server's responses to a local DNS cache so they don't have to query the server every time. To see the DNS cache on Windows, enter the command `ipconfig /displaydns`. To clear the DNS cache, use the command `ipconfig /flushdns`.

#### Cisco IOS

There is no need to configure DNS on routers for hosts to use DNS. Routers just forward DNS messages like any other packets. However, a Cisco router can be configured as a DNS server. If an internal DNS server is used, usually it's a Windows or Linux server. A Cisco router can also be configured as a DNS client. To configure a router as a DNS server:

1. Configure the router to act as a DNS server - `ip dns server`.
2. Configure a list of hostname/IP address mappings - `ip host` followed by the hostname and IP address.
3. Configure a DNS server that the router will query if the requested record isn't in its host table - `ip name-server` followed by the DNS server IP address.
4. Enable the router to perform DNS queries - `ip domain lookup`. It is enabled by default.

The last two commands shown above are used to configure the router as a DNS client so the router acts as a DNS client in case it doesn't have an entry for the specified name.&#x20;

You can also configure the default domain name with the command `ip domain name` followed by the domain name. The domain name will be automatically appended to any hostnames without a specified domain.&#x20;

The command to view the DNS table on a router is `show hosts`.

<figure><img src=".gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt="summary" width="563"><figcaption><p>Summary</p></figcaption></figure>

{% file src=".gitbook/assets/Day 38 Flashcards - DNS.apkg" %}

{% file src=".gitbook/assets/Day 38 Lab - DNS.pkt" %}

{% embed url="https://youtu.be/7D_FapNrRUM" %}
