---
layout: single
title: "Initial HomeLab setup using Virtualbox"
excerpt_separator: "<!--more-->"
author_profile: true
classes: wide
header:
  image: 
  caption: 
categories:
  - Homelab
tags:
  - Homelab
  - active directory
  - ethical hacking
  - networking
---
As an aspiring cybersecurity professional, hands-on experience is crucial for developing the skills needed for this ever-evolving industry.
I designed this homelab to dive further into network infrastrutures and simulate real-world environments and challenges providing a secure playground for experimentation.

In this post, i'll walk you through the architecture of homelab, which includes **pfSense** acting as a **Double NAT Firewall and Router**, Isolated virtualized environment for penetration testing, **Active Directory** labs, and a **Raspberry Pi 5** running **Kali Linux**. By taking advantage of **virtualization** and using **pfSense** to isolate subnets I created an efficient and scalable homelab.

<figure class ="align-center">
  <img src="/images/homelab.jpg">
</figure>

## Let's break this down!
At the heart of this setup is my **Home Router** which connects to a **Managed Layer 2 Switch**. This switch allows communication between my **Raspberry Pi 5** and the virtualized components running on the **Host PC** Through **VLANs**. I opted for this setup because the **Host PC** is currently my daily computer. Using the switch allows me to create **port-based VLANs**. I created two **VLANs ID**, **VLAN ID 1** is the default and provides internet and **VLAN ID 2** is for my homelab and provides isolated communicaton between my **Raspberry Pi 5** and **Host PC**. Using this allowing me to switch the port number **VLANs ID** running to my **Host PC** back to the port connected to my **Router** when the lab isn't running. I use a **USB Wireless Network Adapter** when the lab is running to provide wifi to the **Host PC** and some virtualized components. 

The **Host PC** is running **VirtualBox** to host multiple virtual machines and a **pfSesnse Firewall/Router**. **pfSense** is attached to four network adapters and plays a crucial role in network segmentation, configured to manage three isolated subnets:
- 10.0.0.1/24 (LAN) Bridged to the Switch: network for basic connectivity and management
- 10.6.6.1/24 (Isolated) Internal Network: A dedicated network isolated from internet access for intentially vulnerable machines
- 10.80.80.1/24 (Active Directory Lab) Internal Network: A simulated enterprise network for configuring and securing Active Directory

## pfSense
I enabled **pfSense ISC DHCP daemon** capabilties for the subnets **LAN** and **Isolated** and disabled it on the Active Directory subnet as the domain controller will act as the DHCP server for this lab.
Below is firewall aliases and rules for each interface:
### Aliases
<figure class ="align-center">
  <img src="/images/homelab-delete.png">
</figure>

### NAT Rules
<figure class ="align-center">
  <img src="/images/">
</figure>

### Isolated Rules
<figure class ="align-center">
  <img src="/images/">
</figure>

### AD_LAB Rules
<figure class ="align-center">
  <img src="/images/">
</figure>