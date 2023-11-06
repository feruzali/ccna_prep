---
description: NTP
---

# Day 37

#### The importance of time

All devices have an internal clock. In Cisco IOS, the `show clock` command displays the time.  `*` (asterisk symbol) before the time means that it is not authoritative. The default time zone is **UTC** (Coordinated Universal Time). To see the time source, the `show clock detail` command is used. The default time source is the hardware calendar which is not always accurate. It is important for devices to have an accurate time to have accurate logs for troubleshooting. To see the logs, the command `show logging` is used.&#x20;

#### Manual time configuration

To manually configure time on a device, the command `clock set` followed by time, day, month, and year is used. The hardware and software clock are separate and can be configured separately. The hardware clock is configured the same way but using the command `calendar set`. To synchronize between these two clocks, use the commands:

* `clock update-calendar` - to sync the calendar to the clock's time
* `clock read-calendar` - to sync the clock to the calendar's time

The clock is configured from the privileged EXEC mode but the timezone is configured from the global config mode and becomes the running config of the device. So the command for configuring the timezone is clock timezone followed by a name, hours offset, and minutes offset from UTC.&#x20;

#### Summertime

You can configure automatic DTC (Daylight Saving Time) or Summertime by using the command `clock summer-time` followed by the timezone name and date. To make it recurring, enter `recurring` after the timezone name and specify the start of DST and the end of DST. E.g. `clock summer-time EDT recurring 2 Sunday March 02:00 1 Sunday November 02:00`. In this example, it starts on the 2nd Sunday of March at 2 a.m. and ends on the 1st Sunday of November at 2 a.m. The last option is time offset, the default value is 1 hour.

### NTP

Manually configuring the time on each device is not scalable and takes time. Furthermore, manually configured clocks are hard to synchronize. So, NTP solves this problem. **NTP** (Network Time Protocol) allows automatic time syncing of time over a network. NTP clients request the time from NTP servers. A device can be an NTP server and an NTP client at the same time. NTP allows accuracy of time within \~1 millisecond if the NTP server is in the same LAN or within \~50 milliseconds if connecting to the NTP server over the Internet. NTP uses UDP port 123. The distance of an NTP server from the original **reference clock** is called **stratum**.&#x20;

A reference clock is usually a very accurate time device like an atomic clock or a GPS clock. Reference clocks are stratum 0 within the NTP hierarchy. NTP servers directly connected to reference clocks are stratum 1 (**primary servers**). NTP servers with a stratum higher than 1 are called **secondary servers**.

<figure><img src=".gitbook/assets/image (3) (1).png" alt="ntp heirarchy" width="563"><figcaption><p>NTP Hierarchy</p></figcaption></figure>

Stratum 15 is the maximum. Anything above is considered unreliable. Devices can also peer with devices at the same stratum to provide more accurate time. This is called **symmetric active** mode. An NTP client can sync to multiple NTP servers.&#x20;

#### Configuration

To configure an NTP server on Cisco devices, use the command `ntp server` followed by an IP address of the NTP server. You can configure more than one NTP server on a device, the device selects the best server itself, and others become a backup. To make one of the servers more preferred than others, add the keyword `prefer` after the IP address. To see the NTP servers configured on the device, enter the `show ntp associations` command. To see the details of the currently selected NTP server, enter the `show ntp status` command.&#x20;

NTP uses only the UTC time zone. Appropriate time zones must be configured on each device separately. The `ntp update-calendar` command configures the router to update the hardware clock with the time learned via NTP. To configure an interface as an NTP server, use the command `ntp source` followed by the interface number. For this purpose, loopback interfaces are usually used.

#### Server mode

If there is no NTP server to sync to, and you need to sync the time across all devices in the network, you can make one of the devices an NTP server by using the command `ntp master`. You can also specify the stratum after the command. By default, it is 8.

#### Symmetric active mode

The command to configure symmetric active mode is `ntp peer` followed by the IP address of an NTP server.&#x20;

#### Authentication

NTP authentication can be configured but it is optional. It allows NTP clients to ensure they only sync to the intended servers. To configure NTP authentication:

1. Enable NTP authentication - `ntp authenticate`.
2. Create the NTP authentication key - `ntp authentication-key` followed by a key number, `md5`, and the password (key).
3. Specify the trusted key - `ntp trusted-key` followed by the key number.
4. Specify the key which is needed to use for the server - `ntp server` followed by the server IP address, `key`, and the key number. This command is not needed on the server itself. The same can be applied to peers as well.

<figure><img src=".gitbook/assets/image (2) (1) (1).png" alt="summary" width="563"><figcaption><p>Summary</p></figcaption></figure>

{% file src=".gitbook/assets/Day 37 Flashcards - NTP.apkg" %}

{% file src=".gitbook/assets/Day 37 Lab - NTP.pkt" %}

{% embed url="https://youtu.be/Miys7Ft9wWI" %}
