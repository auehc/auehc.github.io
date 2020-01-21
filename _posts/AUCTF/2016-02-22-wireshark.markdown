---
tagline:  "The Basics of Wireshark"
date:   2016-02-22
categories: archived
author: auctf
tags: wireless
---

This meeting, Matthew gave a quick rundown of Wireshark and it's potential for packet analysis and network sniffing. Wireshark is "the world's foremost network protocol analyzer. It lets you see what's happening on your network at a microscopic level. It is the de facto (and often de jure) standard across many industries and educational institutions." AKA the best thing around for dealing with those weird things called packets.

# Packets

Basically anything that is sent over a network, from ARP messages to visiting HTTP websites to SSHing into another box, is sent using packets. The information or data you're trying to send is split up into packets (the more data, the more packets) that hold the information, as well as needed information for traversing the network and getting to its destination like IP Addresses, MAC addresses, etc. Packets use encapsulation in order to give devices more information on what it's intended to do. Encapsulation is a way to make protocols more modular and works as you move your way up the TCP/IP or OSI model, each layer adding another layer of encapsulation. The "transport" layer of the OSI adds a layer that tells devices what method of transport this packet is using (be it TCP, UDP, etc). These encapsulation layers are important for determining what their purpose was in Wireshark

# Wireshark

Upon opening Wireshark, you have two options: opening up a previous capture file (.pcap, .cap, etc), or beginning your own capture on any interface (the newer versions have a nice graph that show traffic).
![The GUI](/assets/wireshark/wiresharkgui.png)

Everything seems easy until you see the next screen.
![The Mess](/assets/wireshark/wiresharkgui2.png)

What's going on here? Wireshark presents everything to you but if you don't know what you're looking at, it's basically nonsense. This is where the patented "Just look at it" method comes in. A lot of Wireshark knowledge is gained by experience with protocols and filtering techniques. Wireshark has a lot of options to help you along the way, including the ability to filter massive amounts of packets, and follow specific conversations (or streams) of packets. Matthew picked a few examples from previous CTFs to show these off.

The first two, [Sharknado][sharknado] and [Four Eyes][foureyes], are relatively simple. In each scenario you managed to man in the middle some HTTP traffic and are in search of some specific information. In both cases, we are looking for password credentials but due to the differences in the pcap files provided, we have to look for them in different ways. For Sharknado, we need to filter for all the POST requests, since that's how most HTTP login forms work. Typing in 'http.request.method==POST' into the filter bar at the top and search around for post requests containing admin passwords. For Four Eyes, even though we're still looking for passwords, we need one for a specific site (www.2dehands.be) so we'll filter for all conversations with that website. Type 'http.host eq www.2dehands.be' into the filter bar and you'll see a POST request with login credentials.
  
[iSpy][ispy] shows off some of the cooler tools in Wireshark. In this scenario we are looking for important data transfers and are only provided a few packets. Pick one of the HTTP sessions and right click > Follow > TCP Stream. In the window that just opened you'll see mostly garbage, but you might spot some image signatures like PNG. In order to grab all of this data we need to go to File > Export Objects > HTTP > Save All. This should give us a directory of all the files moved across HTTP in this pcap file. Search around and you should find a flag.


[sharknado]: https://github.com/ctfs/write-ups-2015/blob/cce7c49efc641a1c1e848cc06bbac728fd0d6f2d/icectf-2015/forensics/sharknado/README.md
[foureyes]: https://github.com/ctfs/write-ups-2015/blob/4f04788836ab4ce20c9c642088a72ad0aee03a4d/cyber-security-challenge-2015/digital-forensics/four-eyes/README.md
[ispy]: https://github.com/ctfs/write-ups-2015/blob/e20b48e5f0ee72e62177bcb5bcd11f270eaee3f0/easyctf-2015/forensics/ispy/README.md