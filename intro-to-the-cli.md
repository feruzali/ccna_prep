---
description: Day 4
---

# Intro to the CLI

Cisco IOS is an operating system used on Cisco devices (not related to Apple iOS). **CLI** is a command-line interface used to configure Cisco devices. There is also a **GUI** (graphical user interface). Network engineers prefer using CLI over GUI, so GUI will not be covered here.

### CLI connection

To configure a Cisco device with the CLI, we can connect via the console port as below.

<figure><img src=".gitbook/assets/image (76).png" alt="console port" width="375"><figcaption><p>Console ports on Catalyst Switch</p></figcaption></figure>

A cable that can be used to connect to the RJ45 console port is called a rollover cable. And the pins are connected as follows.

<figure><img src=".gitbook/assets/image (100).png" alt="rollover cable" width="375"><figcaption></figcaption></figure>

After the connection is done, we need to use a Terminal emulator like PuTTY and choose a serial connection type to access a CLI.  PuTTY configuration and the default settings for Cisco devices are as follows.

<figure><img src=".gitbook/assets/image (44).png" alt="putty" width="375"><figcaption></figcaption></figure>

### Modes

<figure><img src=".gitbook/assets/image (99).png" alt="cli modes" width="375"><figcaption></figcaption></figure>

#### User EXEC mode

Once you access the CLI, you will be in User EXEC mode by default. It is indicated by the ">" (greater than) sign next to the hostname of the device. User EXEC mode is very limited, users can look at some things but are not allowed to change any configuration. It is also called "user mode".

#### Privileged EXEC mode

To enter Privileged EXEC mode, you have to enter the command `enable` in user mode. It is indicated by the "#" (hashtag) sign next to the hostname. It provides complete access to view the device's configuration, restart it, etc. But the configuration cannot still be changed. [Here](https://www.pcwdld.com/cisco-commands-cheat-sheet) is the list of all available commands. Also, you can use a "?" (question mark) to see the available commands in the current mode.

#### Global configuration mode

The command to enter global configuration mode is `configure terminal`.  The indication of this mode is "(config)" after the hostname. Entering this mode, you can configure the device.

### Password protection

To protect the privileged EXEC mode with a password, we use the command `enable password` followed by the password we want to use. It is case-sensitive. The problem with this command is that it keeps the password unencrypted in the configuration file, to encrypt it, there is another command entered in global configuration mode -`service password-encryption`. But there is an even more secure method, using `enable secret` command instead of `enable password`. In this way, the encryption algorithm used is more advanced. To disable password encryption or cancel any other command, a keyword `no` is used in front of the command. E.g. if we type `no service password-encryption`, future passwords will no longer be encrypted but it doesn't affect the passwords which are already encrypted.

### Configuration files&#x20;

There are two separate configuration files in the device at once:

1. **Running config** - the current, active configuration file on the device. As commands are entered in the CLI, this file gets changed.&#x20;
2. **Startup config** - the configuration file which gets loaded upon the restart of the device.&#x20;

To view the running configuration file, `show running-config` command is used in global configuration mode. For the startup-config file use `show startup-config`.

There are 3 ways to save the running configuration as a startup configuration, and all of them are executed from privileged EXEC mode:

1. `write`
2. `write memory`
3. `copy running-config startup-config`

{% file src=".gitbook/assets/Day 4 Flashcards - Intro to the CLI.apkg" %}

{% file src=".gitbook/assets/Day 4 Lab - Basic Device Security.pkt" %}

{% embed url="https://youtu.be/SDocmq1c05s" fullWidth="false" %}
