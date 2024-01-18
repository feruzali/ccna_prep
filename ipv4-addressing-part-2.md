# IPv4 Addressing (Part 2)

<figure><img src=".gitbook/assets/image (108).png" alt="ipv4 classes table"><figcaption></figcaption></figure>

Class A network is in the range 0-127 but 0 and 127 ranges are reserved, so the usable range of Class A network is 1-126. Let's see one network for calculating the number of usable addresses for hosts. `192.168.1.0/24` is a Class C network so it has a `/24` subnet mask. The host range is `192.168.1.0` - `192.168.1.255`. It gives us 256 (2^8) addresses. But there are network and broadcast addresses, so the total number of usable host addresses is 254. The number of hosts per network is

$$
2^n-2
$$

where `n` is the number of host bits.

### IPv4 Configuration

To check the status of the interfaces on the device, you have to enter `show ip interface brief`  command in privileged EXEC mode. It lists the interface name, IP address, method used to assign, status, and protocol of each interface. The **status** column refers to the Layer 1 state and **protocol** - to the Layer 2 state. The default status of Cisco routers is `administratively down`, it is when the `shutdown` command is applied. Also, you can enter `show interfaces` command but it displays too much information, so it's better to specify an interface using the same command but followed by the interface name. Besides that, you can see the description of each interface, they are optional but might help in identifying the purpose of each interface. The command is `show interfaces description`.

<figure><img src=".gitbook/assets/image (81).png" alt="ip interfaces brief command" width="563"><figcaption></figcaption></figure>

To enter interface configuration mode, you have to enter `interface` followed by the interface name you want to enter in global configuration mode. To configure an IP address - `ip address` followed by the IP address and subnet mask in dot-decimal notation. And lastly, `no shutdown` - to enable the interface. The command to configure the description is `description` followed by the description.

{% file src=".gitbook/assets/Day 8 Flashcards - IPv4 Addresses Part 2.apkg" %}

{% file src=".gitbook/assets/Day 8 Lab - IPv4 Addresses.pkt" %}

{% embed url="https://youtu.be/e1jbvyMeS5I" %}
