---
title:  "Threat Intelligence and Network Analysis Fall 2020"
permalink: /meetings/network_analysis_Fall_2020
tags: meetings
author: therealjman
---

In our meeting on October 13, we discussed threat intelligence and network security.

# Topics

## Threat Intelligence

### APTs

Advanced persistent threats, or APTs for short, are groups that attempt to exploit and maintain access to a system for an extended period of time. These groups are typically nation-states or groups sponsored by them. These threat actors attempt to avoid all suspicion and remain undetected, as they typically have a specific goal they are attempting to achieve. As a result, they are typically very well funded and have skilled people.

### Mitre ATT&CK Framework

The Mitre ATT&CK Framework is a very useful resource for the real world application of cyber threats, acting as a wiki of sorts for analyzing cyber threats. This framework can be used to observe some of the tactics and techniques associated with APTs. Exploiting a system can be like a signature, each group has a slightly different way of doing it and these “signatures” can be used to determine what group committed an attack.

## Network Analysis

### Security Information and Event Management

Security Information and Event Management, more commonly known as SIEM, are software services that are focused on collecting data to one central location. SIEMs are used to sort and cluster relevant information together about a system, such as network data, machine statuses, and endpoint data. When all this data is collected together, SIEMs are used to assist performing forensics on the data.

### Network IDS/IPS

Two popular ways to monitor a network is with an intrusion detection system (IDS) and an intrusion prevention system (IPS). An IDS is used to monitor a network for potential suspicious activity, such as a violation of a security protocol, and alert an administrator when the activity occurs. Most are either signature or anomaly based. Signature based IDS systems use a preprogrammed list of known attack behaviors to trigger an alert. Anomaly based systems use a model of normal network behavior and trigger an alert when it detects a deviation from that model. An IPS then takes action based on the information from the IDS. Typically this takes the form of sending commands to a firewall, rejecting certain data packets, or even severing a connection completely.

### Honeypots

Honeypots perform a function similar to what their name might suggest. They are simply a trap for malicious hackers or other threat actors. A honeypot mimics a valuable, vulnerable target in order to gain information about an attacker. A common example of this is a database full of garbage information that is used to detect if an attacker has gotten into the network.

### OSI Network Model

There are a few different models used for mapping a network, but one of the most popular models is the OSI model. It consists of multiple different layers, with the lower layers providing services to the higher layers. 

#### Application Layer

The top level layer in the OSI model is the application layer, which provides services to application programs. This layer directly interacts with the data from the user and relies on all the lower layers to function. Common protocols that utilize the application layer are HTTP, HTTPS, FTP, SSH, and DNS.

#### Transport Layer

The transport layer is a layer down from the application layer and handles end-to-end communication between devices. There are two main protocols for this layer, TCP and UDP. TCP is a connection oriented protocol, it uses a three way handshake to ensure that packets are delivered in order and are not dropped. It provides reliable transfer of data at the cost of more delay and overhead. UDP does not do any of the packet checking that TCP does, so it is more useful when it does not matter if packets are dropped or out of order.

#### Network Layer

The network layer is the next layer down, and it facilitates data transfer between two different networks. Data is transferred in the form of packets via network paths. Common network layer protocols are IP and ICMP.

#### Data Link Layer

The data link layer is the lowest layer in the model. It handles moving data in and out of a physical link in the network. Some data link layer protocols include ARP and RARP, which are used to match the MAC address of a device to its IP address.

### Packet Sniffing

Packet sniffing is the practice of gathering, collecting, and logging packets that pass through a computer network. There are two main ways to capture packets, hardware or software. Hardware packet sniffers are designed to be physically connected to a network to examine it. Software packet sniffers change the configuration so that the network interface passes all network traffic up the stack, which is also known as promiscuous mode.

# Slideshow
<iframe src="//docs.google.com/gview?url=http://auehc.github.io/assets/powerpoints/Threat_Intel_and_Network_Analysis_10_13_20.pptx&embedded=true" style="width:600px; height:500px;" frameborder="0"></iframe>


