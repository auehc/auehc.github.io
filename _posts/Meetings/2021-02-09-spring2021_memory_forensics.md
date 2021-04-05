---
title:  "Memory Forensics Spring 2021"
permalink: /meetings/Memory_Forensics_Spring_2021
tags: meetings
author: therealjman
---

For our third meeting of the semester, we discussed Windows memory forensics.

# Topics

## Order of Volatility

In the context of digital forensics, different systems on a computer have different levels of volatility. Request for Comment (RFC) 3227 published by the Internet Engineering Task Force outlines that data collection should be performed on the most volatile parts of the system first. Computer memory is listed as the second item on that list, right after CPU cache, so it is usually very important to collect it as soon as possible.

## Locard's Exchange Principle

Locard's Exchange Principle states that "the perpetrator of a crime will bring something into the crime scene and leave with something from it, and that both can be used as forensic evidence." While this principle was created for traditional physical evidence, it still very much applies to digital evidence as well. Even if a malicious actor attempts to remove all of their data from a system, they will inevitably leave something behind, whether that is a malicious process or information on what files were recently opened.

## Why Analyze Memory?

Memory can provide a lot of valuable information that can be difficult or impossible to obtain otherwise. Some of the most important information that can be obtained from memory is things like processes, registry information, commands run, and network connections. Much of this information is exclusive to live memory and will not show up on a disk.

## Volatility and Memory Analysis

Volatility is a very popular open-source memory forensics tool that can be used to analyze memory and Windows registries. It supports a wide variety of plugins that add additional functionality. Some useful Volatility commands as well as information about important core Windows processes are listed below.

### Process Analysis Commands

Volatility has a lot of built in commands that are very important for analyzing memory, and below are some of the first ones that should be run when looking at a memory dump. It is easiest to run Volatility if a PowerShell function is defined for it, as this makes running these commands much simpler.

* **imageinfo** - This command provides a lot of useful information such as the date and time when the memory image was taken from the machine, the kernel build identifier, and the recommended profile to use with the image. This is the first command to run when analyzing an image, as this will show what Volatility profile should be used for the rest of the commands.

* **pslist** - This is simply just a flat list of the processes running at the time the memory dump was made. This is typically the second step in analyzing an image, as this can let you spot any obviously malicious processes.

* **pstree** - This also returns the list of running processes at the time of the memory dump, but this command shows the parent/child relationships for each process. This can be useful to see if a process is running under a parent that it is not supposed to, or if there are too many instances of a process running under a parent.

* **psxview** - This performs a very similar function to pslist but it also shows all of the areas in memory where the process is listed. This can prove useful to find hidden processes.

* **psscan** - This searches the entire memory image to find artifacts of a process, in a similar fashion to file carving. This command can find previously terminated processes and processes that were hidden by something like a rootkit. However, this command can take quite a while to run, as it must parse through the entire image and can sometimes lead to false positives.

### Critical System Processes

There are certain processes in Windows that are critical to normal system operation and it is important to know what they are and how many of them should be running. One common trick used to disguise malicious processes is to mimic the name of a good known process (e.g. scvhost.exe instead of svchost.exe). A list of core Windows processes is below, with a number stating how many of them should be running at any given time and a short description of each.

* **Crss.exe (1)** - The client/server runtime subsystem. It is responsible for creating and deleting processes and threads.

* **Services.exe (1)** - The Windows service control manager. It is a list of all Windows services in private memory space. This process should always be the parent of any svchost.exe, spoolsv.exe, and searchindexer.exe and the parent of this process should always be system32.exe.

* **Svchost.exe (any number)** - These services are responsible for implementing shared service processes, where multiple services can share a process to conserve resource consumption. These should always be running under system32.exe and services.exe.

* **Lsass.exe (1)** - The local security authority subsystem process, which enforces security policy, password verification, and creating process tokens. This process stores clear text password hashes, so it is a common target for injection. This process should always have winlogon.exe and wininit.exe as its parents.

* **Winlogon.exe (1)** - The interactive logon prompt, it initiates the screen saver, loads user profiles, and responds to the secure attention sequence. It also monitors files and directories for Windows File Protection.

* **Explorer.exe (1 per user)** - This process handles GUI folder navigation and the start menu. It has access to documents that are open and FTP credentials that are mapped through Windows Explorer.

* **Smss.exe (1)** - A session manager for user-mode processes that start during boot sequences. It is responsible for creating sessions that isolate OS services from users via console or RDP.

* **Other Common Processes** - There are many other processes that can be seen in a memory dump. Some examples might be a mail client, web browsers, Office, or even the memory collection tools themselves.

### Other Useful Commands

Below is another list of Volatility commands and their functions. These are ones that would typically be used a bit farther into an investigation, as they allow for more analysis of specific processes or things such as command history.

* **handles** - This command displays the handles for a given process. A handle is a reference to a resource when an application references a part of memory. It can show files, registry keys, mutexes, and other processes.

* **cmdscan** or **consoles** - Both of these commands show the commands users ran on the system before the memory dump was made. They show the name of the console host process, the name of the application using the console, all of the commands, and the application process handle. The difference between them is ```cmdscan``` only shows the commands that the user ran, while ```consoles``` not only displays the commands ran, but also whatever was printed to the console.

* **svcscan** - This displays all the running services at the time of the memory dump. It shows items such as the display name, the process ID, the path to the binary, and the current status of each service.

* **dlllist** - This is used to display a all of a process's loaded Dynamic Link Libraries (DLLs), which are libraries that are loaded into memory along with a process. This is useful to see if a an attacker injected a malicious DLL into a process.

* **netscan** - This command shows network artifacts in memory for Windows Vista, 2008 Server, and 7 versions. This finds TCP endpoints, UDP endpoints, and UDP listeners and displays information like the local and remote IP, local and remote port, and the time the connection was established.

* **dump commands** - There are multiple commands in Volatility to dump files. These are useful because sending kernel drivers, cached files, or DLL files to their own individual files can make it easier to search for specific information in them. Some common ones are as follows: ```moddump``` dumps extracts kernel drivers, ```procdump``` dumps a certain process's executable, and ```dlldump``` can be used to dump DLL files.

### Registry

We finished our discussion on Volatility and how to use it to analyze memory with a short look at how Volatility can be used to look at the Windows registry. The Windows registry is a "central hierarchical database used to store information that is necessary to configure the system for one or more users, applications, and hardware devices.” Volatility has several commands to look at registry, with some important ones being ```autoruns```, ```userassist```, and ```shellbags```. The Windows registry is very complicated, so we may cover it in another discussion at a later date.

# Slideshow

<iframe src="//docs.google.com/gview?url=http://auehc.github.io/assets/powerpoints/Memory_Forensics_Spring2021.pptx&embedded=true" style="width:600px; height:500px;" frameborder="0"></iframe>
