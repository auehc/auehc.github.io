---
layout: post
tagline:  "Kickoff Meeting / Kali Linux"
date:   2016-01-25
categories: Meetings
---

In the first AUCTF meeting we went over the basics of what CTFs are, and then talked about the major suite of tools we use for competitions: Kali Linux.

# What's a CTF?

Cyber Security is one of the fastest growing career fields right now, but getting practice hacking things and figuring out new skills will lead to legal trouble if you do things you're not supposed to, and get tedious due to the lack of
competitive space. This is where Security Capture the Flags (CTFs) come in. 

CTFs are a Jeopardy-style competition where teams compete to find 'flags' by solving problems in a number of security related categories that can range from something as simple as nerd-culture [trivia][hack-the-planet] to cryptography to binary exploitation and reverse engineering to social engineering and OpSec.

We use a number of sites in order to practice for competitions. The best site for writeups and upcoming CTFs is [ctftime][ctftime]. Some of the best legal areas to practice are things called wargames (always active ctfs) which can be found at sites like [Hack This Site][hackthissite], [Over The Wire][overthewire], and [PicoCTF][picoctf].

---

# Kali Linux

Kali is an operating system that comes with a bunch of penetration testing tools built in, based on its successor 'BackTrack'; bootable off a flash drive or in a Virtual Machine and is one of the best things available to get started in hacking and CTFs. An iso to build for VMs is readily availabe on [Offensive Security's][offensive] website.

Some of the most used tools inclue:

Web Applications | Passwords  | Reversing  |  Forensics  | Networks/Wireless
-----------------|------------------|------------|-------------|------------------
   BurpSuite     |  John the Ripper |   OllyDbg  |  BinWalk    |     Wireshark  
   OWASP-Zap     |     Ophrack      |   Radare2  |  Foremost   |    Aircrack-ng
    HTTrack      |     Hashcat      |   IDA Pro  |  Scalpel    |       nmap
    SQLmap       |     Medusa       |   Dex2Jar  |MagicRescue |
    			 |	 RainbowCrack   |   APKTool  | Volatility  |

  
---  
  
We'll go over most of these tools in depth over the semester.

[Slides](/assets/powerpoints/KaliPresentation.odp)

[hack-the-planet]: http://d.ibtimes.co.uk/en/full/1415646/hack-planet-2014-year-hackers-took-control.png?w=736
[ctftime]: https://ctftime.org
[hackthissite]: https://www.hackthissite.org/
[overthewire]: http://overthewire.org/wargames/
[picoctf]: https://picoctf.com/problems
[offensive]: https://www.offensive-security.com/kali-linux-vmware-virtualbox-image-download/