---
description: Software-Defined Networking
---

# Day 62

<figure><img src=".gitbook/assets/image.png" alt="SDN layers" width="563"><figcaption></figcaption></figure>

The **application layer** contains scripts/applications that tell the SDN controller what network behaviors are desired. The **control layer** contains the SDN controller that receives and processes instructions from the application layer. The **infrastructure layer** contains the network devices that are responsible for forwarding messages across the network.

### SD-Access

Cisco **SD-Acces** is Cisco's SDN solution for automating campus LANs. **ACI** (Application Centric Infrastructure) is their SDN solution for data centers, **SD-WAN** - for WANs. Cisco **DNA** (Digital Network Architecture) Center is the controller at the center of SD-Access.

<figure><img src=".gitbook/assets/image (1).png" alt="DNA Center" width="563"><figcaption></figcaption></figure>

The **underlay** is the underlying physical network of devices and connections (wired and wireless) which provide IP connectivity (multilayer switches and their connections).&#x20;

<figure><img src=".gitbook/assets/image (3).png" alt="underlay " width="563"><figcaption></figcaption></figure>

The **overlay** is the virtual network built on top of the physical underlay network. SD-Access uses VXLAN (Virtual Extensible LAN) to build tunnels.&#x20;

<figure><img src=".gitbook/assets/image (5).png" alt="overlay" width="563"><figcaption></figcaption></figure>

The **fabric** is the combination of the overlay and underlay - the physical and virtual network as a whole.&#x20;

<figure><img src=".gitbook/assets/image (6).png" alt="fabric" width="563"><figcaption></figcaption></figure>

#### Underlay

The underlay's purpose is to support the VXLAN tunnels of the overlay. There are 3 different roles for switches in SD-Access: **Edge nodes** - connect to end hosts, **Border nodes** - connect to devices outside of the SD-Access domain (ie WAN routers), **Control nodes** - use **LISP** (Locator ID Separation Protocol) to perform various control plane functions.

SD-Access can be configured on top of an existing network (**brownfield deployment**) if the network hardware and software support it. But in this case, DNA Center won't configure the underlay. A new deployment (**greenfield deployment**) is configured by DNA Center to use the optimal SD-Access underlay. In this case, all switches are Layer 3 and use IS-IS as their routing protocol, all links between switches are routed ports, so no STP is needed. Edge nodes (access switches) act as the default gateway of end hosts (**routed access layer**).

<figure><img src=".gitbook/assets/image (4).png" alt="SD-Access Underlay" width="563"><figcaption></figcaption></figure>

#### Overlay

LISP provides the control plane of SD-Access. A list of mappings of **EID**s (endpoint identifiers) to **RLOC**s (routing locators) is kept. EIDs identify end hosts connected to edge switches and RLOCs identify the edge switch which can be used to reach the end host. **Cisco TrustSec** (CTS) provides policy control (QoS, security policy, etc.). VXLAN provides the data plane of SD-Access.

<figure><img src=".gitbook/assets/image (2).png" alt="overlay demo" width="563"><figcaption></figcaption></figure>

### DNA Center

Cisco DNA Center has two main roles: the SDN controller in SD-Access, and a network manager in a traditional network.  DNA Center is an application installed on Cisco UCS server hardware. The **SBI** (SelfBound Interface) supports protocols like NETCONF and RESTCONF (as well as Telnet, SSH, and SNMP). DNA Center enables **IBN** (Intent-Based Networking). The goal is to allow the engineer to communicate their intent for network behavior to the DNA Center, and then the DNA Center takes care of the details of the actual configuration and policies on devices (ie ACLs).

{% file src=".gitbook/assets/Day 62 Flashcards - SDN.apkg" %}
