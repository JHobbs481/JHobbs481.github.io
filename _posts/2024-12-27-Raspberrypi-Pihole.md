---
layout: single
title: "Pi-Hole setup on a Raspberry pi zero 2W"
excerpt_separator: "<!--more-->"
author_profile: true
classes: wide
header:
  image: images/raspberrypibanner.png
  caption: "[Raspberry Pi](https://www.raspberrypi.com/)"
categories:
  - Raspberry Pi
tags:
  - Ad blocker
  - raspberry pi
---
Hello, and welcome to my first project working with a Raspberry Pi unit. Today I will be installing [Pi-Hole](https://pi-hole.net/) on my **Raspberry Pi Zero 2W** to hopefully get rid of those pesky ads.

If you have never heard of [Pi-Hole](https://pi-hole.net/), then let me briefly explain what it is.
**Pi-hole** is a **linux network-level** ad and internet tracker blocking application which acts as a **DNS sinkhole** with the option of being a **DHCP server**.

I decided to go with the **Raspberry Pi Zero 2W** due to the amount of devices connected to my network.
However, in the future I want to upgrade to a **Raspberry Pi 4** to install softwares like [Home Assistant](https://www.home-assistant.io/).

## Let's Begin:

I started by using the [Raspberry Pi Imager](https://www.raspberrypi.com/software/) provided by Raspberry pi, to install **Raspberry PI OS (64-BIT)** operating system on my Micro SD card.

<figure class ="align-center">
	<img src ="/images/raspberrypi-imager.PNG">
</figure>

After that, I installed the Micro SD into the **Raspberry Pi** and powered it on.
I then logged into the admin page of my router to issue a **Static IP** to the device in the event it goes offline.
Then I changed the **DNS gateway** to the IP of the **Raspberry Pi** in order for **Pi-Hole** to work.

Next, I used a terminal emulator called [Putty](https://www.putty.org/) to **ssh** into the **Raspberry Pi** and install **Pi-Hole** using their one liner quick installer.

```console
curl -sSL https://install.pi-hole.net | bash
```
Once finished, It provides a url to access the admin page of **Pi-Hole**.
<figure class ="align-center">
	<img src ="/images/Piholeadminpage.PNG">
</figure>

As a result, I can see the device is connected and working properly. Furthermore, we can add blocklists under the Adlists tab and view the query logs to help troubleshoot any issues.

Additionally, I used a blocklist collection made by [Firebog](https://firebog.net/) to add a couple categories such as **Advertising**, **Malicious**, and **Tracking & Telemetry** **lists** onto my **Pi-Hole**.
I then used **Putty** to ssh back into my **Raspberry Pi** and ran the command `pihole -g` to officially add the blocklists previously inputted.

<figure class ="align-center">
	<img src ="/images/Piholeadlist.PNG">
</figure>

## Conclusion:
We are finished\! This was a very easy beginner project working with a **Raspberry Pi** device.
There are too many benefits for running **Pi-Hole** on your **home network** to list here, but I highly suggest researching and adding this to your arsenal.

Now that we have **Pi-Hole** up and running we can test a website I know has ads and see if they get blocked.
For this demonstration I used a website called [Hackaday](https://hackaday.com/) to display a before and after image.

### Before:
<figure class ="align-center">
	<img src ="/images/hackadaybefore.PNG">
</figure>

### After:
<figure class ="align-center">
	<img src ="/images/hackadayafter.PNG">
</figure>

