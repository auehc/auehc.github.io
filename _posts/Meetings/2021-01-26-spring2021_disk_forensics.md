---
title:  "Disk Forensics Spring 2021"
permalink: /meetings/Disk_Forensics_Spring_2021
tags: meetings
author: therealjman
---

For the first topic of the new year, we covered disk forensics. We discussed the layouts of common file systems and how to locate and recover files from them.

# Topics 

## File Systems

Two of the most common file systems are FAT16, which was used on legacy systems, and the New Technology File System (NTFS), which is used on Windows and some Linux machines. However, before we cover the details of each file system, there is some basic information and terms that need to be explained.

### Disk Hierarchy

A disk is broken down into a hierarchy of components. The disk is the highest level, storing the data as physical 1s and 0s. Then each disk is usually separated into one or more logical partitions. Each partition is set up with a particular file system, which controls the way information is stored and retrieved. A data unit is a group of consecutive sectors that hold file contents. Then each individual file has metadata which is data that describes the file, such as the file name, date it was created, and other things.

### Terms

There are some important terms to know when discussing disk forensics. A sector is the smallest unit on a disk, this is typically 512 bytes but that number can change. A cluster is simply a group of consecutive sectors. A Little Endian number is a hexadecimal number where the least significant byte is stored at the smallest address. A Big Endian number is a hex number where the most significant byte is stored at the smallest address.

## FAT16 File System

The FAT16 file system is an old system that is not used very much anymore, but used to be more popular. FAT16 gets its name from use of the File Allocation Table (FAT), which contains a list of data clusters that hold file contents.

### Architecture

A FAT16 partition is made up of multiple dedicated sections. The first part, the reserved area or the boot sector, contains information such as the number of FATs, sector size, and sectors per cluster. Then the first FAT area is simply the location of the first FAT on the disk. Then there is also a second FAT, which serves as a backup of the first one. The root directory then contains information such as filenames, file size, and the file starting cluster. Finally, the data area contains the actual file data.

### File Recovery Process

The first step in analyzing a FAT16 partition is to get the useful information from the boot sector such as bytes per sector, sectors per cluster, and the number and location of the FATs. Then the FAT should be looked at to determine the number of files on the partition. Next, you would look at the root directory to find out the starting locations and size of each file. Once the starting sector and size of each file is known, you can use the *dd* command in Linux to carve the file from the disk.

## NTFS File System

The NTFS file system is much more modern and complex than FAT16, and is used in many modern systems. It allows for much larger partitions, file sizes, and has more security features when compared to FAT16.

### Architecture

A NTFS partition is also made up of multiple sections. The beginning of the partition is made up of disk information. Then the NTFS partition is made up of multiple different components, the Master Boot Record (MBR), the Master File Table (MFT), the MFT backup, and the file data area. The MBR contains a partition table and contains information similar to the FAT boot sector. The MFT is comprised of 1024-byte entries for every data object in the file system, including files, folders, and applications. The backup MFT is exactly what it sounds like, a backup of the MFT in case the first one becomes corrupt. Then the data section is what contains the actual file and application data.

### MFT

The MFT is where the bulk of a forensicist's time will be spent while analyzing an NTFS drive. Each MFT entry is 1024 bytes long, where the first 512 bytes are the file metadata attributes. Elements such as a file's name, data, creation and modification time, and security information are all file attributes. For files that are less than 512 bytes in size, termed resident files, the actual file data can be stored in the second 512 bytes of the MFT. For NTFS drives formatted using Windows, the first 39 entries are reserved for system files and for drives formatted using Linux, the first 64 entries are reserved.

### File Recovery Process

The first step in recovering files off a NTFS partition would be to determine where the partition begins. Then, you would look at the MBR to determine information such as bytes per sector and where the MFT entries begin. Then, you would determine where the system generated MFT entries and identify the user-generated entries. Then you would look at the file attributes to determine whether the files are resident or non-resident files. Also using the MFT attributes, you would determine the starting cluster and size of each non-resident file. Then once this information is known, you can use the *dd* command to carve the files in the same you would for a FAT partition.

# Slideshow
<iframe src="//docs.google.com/gview?url=http://auehc.github.io/assets/powerpoints/Disk_Forensics_Spring2021.pptx&embedded=true" style="width:600px; height:500px;" frameborder="0"></iframe>
