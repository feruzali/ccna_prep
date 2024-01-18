---
description: Day 48
---

# Security Fundamentals

The principles of the **CIA Triad** from the foundation of security:

* **Confidentiality**: Only authorized users should be able to access data.&#x20;
* **Integrity**: Data should be correct and authentic. Data should not be modified by unauthorized users.
* **Availability**: The network should be operational and accessible to authorized users.

A **vulnerability** is a potential weakness that can compromise the CIA of a system. An **exploit** is something that can potentially be used to exploit the vulnerability. A **threat** is the potential of a vulnerability to be exploited. A **mitigation technique** is something that can protect against threats.

### Common Attacks

#### DoS

**DoS** (Denial of Service) attacks threaten the availability of a system. One common DoS attack is the TCP SYN flood. The attacker sends countless TCP SYN messages to the target. The target replies with SYN-ACK messages but the attacker never sends the final ACK message so the target's TCP connection table gets filled up and it is no longer able to make legitimate TCP connections.&#x20;

<figure><img src=".gitbook/assets/image (154).png" alt="TCP SYN flood demo" width="563"><figcaption></figcaption></figure>

In a **DDoS** (Distributed Denial of Service) attack, the attacker infects many target computers with malware and uses them to initiate a DoS attack. The group of infected computers is called a **botnet**.

#### Spoofing

To spoof an address is to use a fake source address. There are a lot of attacks which involve spoofing. One of them is **DHCP exhaustion**. An attacker uses spoofed MAC addresses to flood DHCP Discover messages. The target's DHCP pool becomes full and results in a DoS.

<figure><img src=".gitbook/assets/image (155).png" alt="DHCP exhaustion demo" width="563"><figcaption></figcaption></figure>

#### Reflection/Amplification

In a reflection attack, the attacker sends traffic to a reflector (i.e. DNS server) and spoofs the source address using the target's IP address. The reflector then sends reply messages to the target's IP address. If the amount of traffic is large enough, it may cause a DoS. A reflection attack becomes an amplification attack when the amount of traffic sent by an attacker is small but it triggers the large amount of traffic to be sent from the reflector to the target.

<figure><img src=".gitbook/assets/image (156).png" alt="reflection attack demo" width="563"><figcaption></figcaption></figure>

#### MITM

In a man-in-the-middle attack, the attacker places himself between the source and destination to eavesdrop on communications, or to modify traffic before it reaches the destination. One of the common attacks is **ARP spoofing** (aka **ARP poisoning**). When the target sends an ARP Request, the attacker replies with an ARP Reply spoofing the legitimate replier's address. The attacker overwrites the legitimate entry in the target's ARP table. The attacker can inspect and modify the message compromising the Confidentiality and Integrity of communications between the target and legitimate server.

<figure><img src=".gitbook/assets/image (153).png" alt="mitm demo" width="563"><figcaption></figcaption></figure>

#### Reconnaissance

Reconnaissance attacks are not attacks themselves but they can be used to gather information about a target which can later be used for future attacks. This is often publicly available information, i.e. `nslookup` to learn the IP address of a website.&#x20;

#### Malware

**Malware** (malicious software) refers to a variety of harmful programs that can infect a computer. **Viruses** infect other software (**host program**). The virus spreads as the software is shared by users. Typically they corrupt or modify the files on the target computer. **Worms** don't require a host program. They are standalone malware and are able to spread on their own, without user interaction. The spread of worms can congest the network but the payload of a worm can cause additional harm to target devices. **Trojan Horses** are harmful software that is disguised as legitimate software. They are spread through user interaction such as opening email attachments, downloading a file from the internet, etc.&#x20;

#### Social Engineering

Social Engineering attacks target the most vulnerable part of any system - people. They involve psychological manipulation to make the target reveal confidential information or perform some action. &#x20;

* **Phishing** typically involves fraudulent emails that appear to come from a legitimate source and contain links to a fraudulent website that seems legitimate. Users are asked to log in to the website compromising their credentials. **Spear phishing** is a more targeted form of phishing, i.e. aimed at employees of a particular company. **Whaling** is phishing targeted at high-profile individuals, i.e. a company president. **Vishing** (voice phishing) is phishing performed over a phone call. **Smishing** (SMS phishing) is phishing using text messages.&#x20;
* **Watering hole** attacks compromise sites that the target victim frequently visits. If a malicious link is placed on a website the target trusts, they might not hesitate to click.
* **Tailgating** attacks involve entering restricted, secured areas by simply walking in behind the authorized person as they enter.

#### Password attacks

Most systems use username/password combination to authenticate. The username is often easy to guess and the strength of the password is relied on to provide the necessary security. Attackers can learn the user's password via multiple methods:

* Guessing
* **Dictionary attack** - a program runs through a list of common words/passwords to find the target's password.
* **Brute force attack** - a program tries every possible combination of letters, numbers, and special characters to find the target's password.

A strong password should contain at least 8 characters, a mixture of uppercase and lowercase letters, a mixture of letters and numbers, and one or more special characters. Also, it should be changed regularly.&#x20;

### Multi-factor Authentication

Multi-factor authentication involves providing more than just a username/password to prove your identity. It increases security. It usually involves providing two of the following:

* Something you know - username/password, PIN code, etc.
* Something you have - pressing a notification on the phone, a badge that is scanned, etc.
* Something you are - biometrics like a face scan, fingerprint scan, etc.

### Digital Certificates

Digital certificates are another form of authentication used to prove the identity of the holder of the certificate. They are used for websites to verify that the website being accessed is legitimate. Entities that want a certificate to prove their identity send a **CSR** (Certificate Signing Request) to a **CA** (Certificate Authority) which generates and signs the certificate.&#x20;

### AAA

**AAA** stands for Authentication, Authorization, and Accounting. It is a framework for controlling and monitoring users of a computer system. **Authentication** is a process of verifying a user's identity (logging in). **Authorization** is a process of granting the user the appropriate access and permissions. **Accounting** is a process of recording the user's activities on the system. Enterprises typically use a AAA server to provide AAA services. Cisco's AAA server is **ISE** (Identity Services Engine). AAA servers usually support the following two AAA protocols:

* **RADIUS** - an open standard protocol. Uses UDP ports 1812 and 1813.
* **TACACS+** - a Cisco proprietary protocol. Uses TCP port 49.

### Security Program&#x20;

**User awareness** programs are designed to make employees aware of potential security threats and risks. For example, a company might send out false phishing emails to make employees click a link and sign in with their credentials.&#x20;

**User training** programs are more formal than user awareness programs. For example, dedicated training sessions which educate users on corporate security policies, how to create strong passwords, and how to avoid potential threats.

**Physical access control** protects equipment and data from potential attackers by only allowing authorized users into protected areas such as network closets or data center floors. Multifactor locks can protect access to restricted areas.

{% file src=".gitbook/assets/Day 48 Flashcards - Security Fundamentals.apkg" %}

{% embed url="https://youtu.be/EBs47-0ZD-A" %}
