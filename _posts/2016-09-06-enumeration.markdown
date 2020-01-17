---
layout: post
tagline:  "First Meeting - Enumeration on a network"
date:   2016-09-06
categories: Meetings
---

[Slides](/assets/powerpoints/Enumeration-Presentation2.pptx)

Late on posting this; my bad.  

On the 6th we went over the basics of networking as well as some tools for network enumeration.  

The basics of networking included how routing works, protocols, and the OSI model; which is all easily googlable.  

For enumeration, we started at the most basic tools: ping and traceroute which are usually network testing / administration tools but can be used to check if systems are live (unless ICMP is blocked). Then we moved onto host discovery with arp (which only works same-subnet) using tools like arp-scan and netdiscover.   

We then talked about port scanning, the bread and butter of information gathering. The most commonly used tool for this is nmap, a decade old tool with every option you would need for port scanning. We talked about a number of flags but it's worth looking up a cheat-sheet and getting comfortable with the common ones (-p -sV -A -sU etc). This is easily testable with some virtual machines at home. Some alternative port scanning tools include zenmap, sparta, or mass-scan.  

Host discovery and network enumeration are the most important steps of hacking anything so it's important to gain a good foundation. Next time we'll leverage this for actual exploitation.  


Tools Used:  
ping  
traceroute/tracert  
arp-scan / netdiscover  
nmap / zenmap  
sparta  
mass-scan  
shodan.io