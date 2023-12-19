---
description: Wireless Fundamentals
---

# Day 55

### Wireless LANs

Wireless LANs are defined in IEEE 802.11. Wireless networks have some issues that we need to deal with.&#x20;

* All devices within range receive all frames like devices connected to an Ethernet hub. Privacy of data within the LAN is a greater concern. **CSMA/CA** (Carrier Sense Multiple Access with Collision Avoidance) is used to facilitate half-duplex communications. When using CSMA/CA, a device waits for other devices to stop transmitting before it transmits data itself.
* Wireless communications are regulated by various international and national bodies.
* Wireless signal coverage area must be considered.
* Other devices using the same channels can cause interference.

The factors which affect signal transmission range:

*   **Absorption** - happens when a wireless signal passes through a material and is converted into heat weakening the original signal.\


    <figure><img src=".gitbook/assets/image (6) (1).png" alt="absorption " width="563"><figcaption></figcaption></figure>
*   **Reflection** - happens when a signal bounces off of a material like metal.\


    <figure><img src=".gitbook/assets/image (7) (1).png" alt="reflection" width="563"><figcaption></figcaption></figure>
*   **Refraction** - happens when a wave is bent when entering a medium where the signal travels at a different speed.\


    <figure><img src=".gitbook/assets/image (8) (1).png" alt="refraction" width="563"><figcaption></figcaption></figure>
*   **Diffraction** - happens when a wave encounters an obstacle and travels around it. This can result in blind spots behind the obstacle.\


    <figure><img src=".gitbook/assets/image (9) (1).png" alt="diffraction" width="563"><figcaption></figcaption></figure>
*   **Scattering** - happens when a material causes a signal to scatter in all directions. Dust, smog, uneven surfaces, etc. can be a cause of scattering.\


    <figure><img src=".gitbook/assets/image (10) (1).png" alt="scattering" width="563"><figcaption></figcaption></figure>

### Radio Frequency

To send wireless signals, the sender applies an alternating current to an antenna. This creates electromagnetic fields (waves). Electromagnetic waves can be measured in multiple ways:

*   **Amplitude** - maximum strength of the electric and magnetic fields.\


    <figure><img src=".gitbook/assets/image (11).png" alt="amplitude" width="563"><figcaption></figcaption></figure>
*   **Frequency** - number of up/down cycles per a given unit of time. Measured in hertz (Hz) - cycles per second.\


    <figure><img src=".gitbook/assets/image (12).png" alt="frequency" width="563"><figcaption></figcaption></figure>

A **period** is the amount of time of one cycle, e.g. if the frequency is 4 Hz, the period is 0.25 seconds.

Wi-Fi uses two main bands (frequency ranges): **2.4 GHz** and **5 GHz**. The 2.4 GHz band provides further reachability in open space and better penetration of obstacles like walls. Since many devices use a 2.4 GHz band, interference can be a problem compared to a 5 GHz band. **Wi-Fi 6** has expanded the spectrum range to include a band in the 6 GHz range.&#x20;

### Channels

Each band is divided up into multiple channels. Devices are configured to transmit and receive traffic on one or more of these channels. The 2.4 GHz band is divided into several channels, each with a 22 MHz range but channels may overlap each other. In a small wireless LAN with only a single AP, any channel can be used. However, in large WLANs with multiple APs, adjacent APs mustn't use overlapping channels to avoid interference. In the 2.4 GHz band, it's recommended to use channels **1, 6, and 11**. The 5 GHz band consists of non-overlapping channels, so it's much easier to avoid interference. To provide full coverage of an area without band interference, a honeycomb pattern might be used. Each color in the picture below represents a different channel.

<figure><img src=".gitbook/assets/image (10).png" alt="honeycomb pattern" width="375"><figcaption></figcaption></figure>

Below is a table with different 802.11 standards:

| Standard           | Frequencies     | Max Data Rate |
| ------------------ | --------------- | ------------- |
| 802.11             | 2.4 GHz         | 2 Mbps        |
| 802.11b            | 2.4 GHz         | 11 Mbps       |
| 802.11a            | 5 GHz           | 54 Mbps       |
| 802.11g            | 2.4 GHz         | 54 Mbps       |
| 802.11n (Wi-Fi 4)  | 2.4 / 5 GHz     | 600 Mbps      |
| 802.11ac (Wi-Fi 5) | 5 GHz           | 6.93 Gbps     |
| 802.11ax (Wi-Fi 6) | 2.4 / 5 / 6 GHz | 4 \* 802.11ac |

### Service Sets

802.11 defines different kinds of service sets which are groups of wireless network devices. All devices in a service set share the same **SSID** (Service Set Identifier) The SSID is a human-readable name which identifies the service set. The SSID doesn't have to be unique. There are three main types of service sets: Independent, Infrastructure, and Mesh.

* **IBSS** (Independent Basic Service Set) - wireless network in which two or more devices connect directly without using an AP (Access Point). Also known as an **ad hoc** network. It is not scalable beyond a few devices and is mainly used for file transfer.
* **BSS** (Basic Service Set) - a kind of Infrastructure Service Set in which clients connect via an AP but not directly to each other. A BSSID (Basic Service Set ID) is used to uniquely identify the AP. Other APs can use the same SSID but not the same BSSID because the BSSID is the MAC address of the AP's radio. To be a part of the BSS, wireless devices request to associate with the BSS and are called clients/stations. The physical area around an AP where its signal is usable is called a **BSA** (Basic Service Area), BSS is a group of devices.
* **ESS** (Extended Service Set) - a larger WLAN beyond the range of a single AP. APs with their BSSs are connected by a wired network. Each BSS uses the same SSID but a unique BSSID. Also, each BSS uses a different channel to avoid interference. Clients can pass between APs without having to reconnect, providing a seamless Wi-Fi experience when moving between APs - **roaming**. To make it possible, the BSAs should overlap about 10-15%.
* **MBSS** (Mesh Basic Service Set) can be used in situations where it is difficult to run an Ethernet connection to every AP. Mesh APs use two radios: one to provide a BSS to wireless clients, and one to form a backhaul network which is used to bridge traffic from AP to AP.  At least one AP is connected to the wired network and is called **RAP** (Root Access Point), other APs are called **MAP**s (Mesh Access Points).

### Distribution System

Most wireless networks are not standalone networks, they are just a way for wireless clients to connect to the wired network infrastructure. In 802.11, the upstream wired network is called the **DS** (Distribution System). Each wireless BSS or ESS is mapped to a VLAN in the wired network.

An AP can also provide multiple WLANs, each with a unique SSID. Each WLAN is mapped to a separate VLAN and connected to the wired network via a trunk. Each WLAN uses a unique BSSID, usually by incrementing the last digit of the BSSID by one.

### AP Operational Modes

APs can operate in additional modes:

*   **Repeater** - can be used to extend the range of BSS. The repeater simply retransmits any signal it receives from the AP. A repeater with a single radio must operate on the same channel as the AP but this can reduce the overall throughput on the channel. A repeater with two radios can solve this issue.\


    <figure><img src=".gitbook/assets/image (2) (1).png" alt="repeater demo" width="563"><figcaption></figcaption></figure>
*   **WGB** (Workgroup Bridge) - operates as a wireless client of another AP and can be used to connect wired devices to the wireless network. uWGB (universal WGB) is an 802.11 standard that allows one device to be bridged to the wireless network. WGB is a Cisco-proprietary version of the 802.11 standard that allows multiple wired clients to be bridged to the wireless network.\


    <figure><img src=".gitbook/assets/image (3) (1).png" alt="WGB demo" width="563"><figcaption></figcaption></figure>
*   **Outdoor bridge** can be used to connect networks over long distances without a physical cable connecting them. The APs use specialized antennas that focus most of the signal power in one direction which allows the wireless connection to be made over longer distances than normally possible. The connection can be point-to-point or point-to-multipoint.\


    <figure><img src=".gitbook/assets/image (4) (1).png" alt="outdoor bridge demo" width="563"><figcaption></figcaption></figure>

{% file src=".gitbook/assets/Day 55 Flashcards - Wireless Fundamentals.apkg" %}
