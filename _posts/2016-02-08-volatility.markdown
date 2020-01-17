---
layout: post
tagline:  "Memory Forensics with Volatility"
date:   2016-02-08
categories: Meetings
---

The second half of the third meeting of the semester focused on memory forensics. We discussed what memory forensics is and looked at Volatility, the front-runner for memory and disk analysis.


# What is memory forensics?

Imagine you work for a police station or the FBI and you find the laptop of a hacker still running. How do you figure out what he was doing and what's on his laptop without tampering with the original hardware and potentially setting off any traps he might have enabled? Instead of potentially screwing everything up by playing with the original machine, you take all of the information about the box and shove it into a .img or .mem file. This "information" includes processes, files, policies, users, registry information, settings, etc. That's the basis for memory forensics.

# Volatility

Volatility is the premier memory analysis tool for disk images and memory files. It is an open source python based tool that comes natively on Kali and can be used to find any of the information listed above with just a few simple commands on supported files. It supports most major operating systems from 32-bit Windows XP SP2 to 4.2.3+ Linux Kernels to El Capitan.

The imageinfo module can be used to find out hardware information, the operating system / profiles, and datetime settings. 

	volatility imageinfo -f memfile.mem

The psscan and pslist modules will list out all process information when the snapshot was taken, including PIDs, associated executables, and start times. Basically anything your process manager would tell you.

	volatility psscan -f memfile.mem
	volatility pslist -f memfile.mem

There are a number of modules for finding out random information. Clipboard can be used to find what was currently copied to user clipboards. Connection gives you basic information about networking, like what the box was plugged into. Malfind runs a signature based detection in order see if malware was on the machine. Finally, crashfind and hibfind give you shutdown information about the machine.

	volatility clipboard -f memfile.mem
	volatility connections -f memfile.mem
	volatility malfind -f memfile.mem
	volatility crashfind -f memfile.mem
	volatility hibfind -f memfile.mem

One of the most useful tools from a CTF standpoint is the ability to peruse through the registry of Windows boxes using Volatility's hivelist, printkey, hivedump, and hashdump modules.

*	Hivelist will list available 'hives' which are groups of keys like SAM or Security.
*	PrintKey will use a given hivelist to print a specific key, like an administrative template setting or user's password hint.
*	Hivedump will print all keys and subkeys in a hive
*	Hashdump will dump any NTLM or Lanman hashes found in a hive

For example, we can use all of these modules in order to get the password hashes of all the users on an XP box in order to crack them.

First, we need information about the box.

	volatility imageinfo -f memfile.mem

This will tell us possible profiles, in this case WinXPSP2x86 or WinXPSP3x86. Using this profile we can list all the available hives, we are looking for the system hive and the SAM hive's memory addresses.

	volatility hivelist --profile=WinXPSP2x86 -f memfile.mem

Now that we have the System memory address (0xe10181f0) and the SAM memory address (0xe1271ae0), we can print the NTLM hashes between them.

	volatility hashdump --profile=WinXPSP2x86 -y 0xe10181f0 -s 0xe1271ae0 -f memfile.mem > hashes.txt

Now, inside the hashes.txt file, there should be a list of NTLM hashes which we can crack with a website like [HashKiller][hashkiller].

Will post pictures/memory file soon.

[Slides](/assets/powerpoints/basics_networks_memory.pptx)

[hashkiller]: https://hashkiller.co.uk/ntlm-decrypter.aspx