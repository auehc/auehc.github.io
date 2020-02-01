---
title:  "Binary Reverse Engineering Resources"
categories: resources 
author: snow
---

Collection of reverse engineering resources from books to challenge sites to tools.

# Learning

## Books

* [Assembly Language for x86 Processors](https://www.amazon.com/Assembly-Language-x86-Processors-Irvine-ebook/dp/B00IZOD46K)
* [Reverse Engineering for Beginners](https://beginners.re/)
* [Practical Malware Analysis](https://www.amazon.com/Practical-Malware-Analysis-Hands-Dissecting/dp/1593272901)
* [Practical Reverse Engineering](https://www.amazon.com/Practical-Reverse-Engineering-Reversing-Obfuscation/dp/1118787315/ref=sr_1_2?crid=3KELEPS7O6WTB&keywords=practical+reverse+engineering&qid=1580518768&s=books&sprefix=practical+rever%2Cstripbooks%2C148&sr=1-2)    
* [Reversing: Secrets of Reverse Engineering](https://www.amazon.com/Reversing-Secrets-Engineering-Eldad-Eilam/dp/0764574817)
* [Malware Analysts Cookbook](https://www.amazon.com/Malware-Analysts-Cookbook-DVD-Techniques/dp/0470613033/ref=sr_1_3?keywords=malware+cookbook&qid=1580518880&s=books&sr=1-3)
* [Radare 2](https://radare.gitbooks.io/radare2book/content/)
* [IDA Pro Book](https://www.amazon.com/gp/product/1593272898/ref=as_li_qf_sp_asin_il_tl?ie=UTF8&tag=s4comecom20-20&camp=1789&creative=9325&linkCode=as2&creativeASIN=1593272898&linkId=19076de758993553eec4d13331a9fffe)

## Courses

* [RPISEC Malware Course](https://github.com/RPISEC/Malware)
* [ARM Assembly Basics](https://azeria-labs.com/writing-arm-assembly-part-1/)

# Sites

## Useful

* [Compiler Visualizer](https://godbolt.org/)
* [x86 Stack Explanation](https://eli.thegreenplace.net/2011/02/04/where-the-top-of-the-stack-is-on-x86/)
* [x86-64 Stack Explanation](https://eli.thegreenplace.net/2011/09/06/stack-frame-layout-on-x86-64)
* [GNU Assembly](https://cs.lmu.edu/~ray/notes/gasexamples/)

## Documentation

* [x86 Assembly High Overview](https://www.aldeid.com/wiki/Category:Architecture/x86-assembly)
* [x86 OP Codes](https://www.aldeid.com/wiki/X86-assembly/Instructions)
* [x86-64 Linux Syscalls](http://blog.rchapman.org/posts/Linux_System_Call_Table_for_x86_64/)
* [x86 Linux Syscalls](https://syscalls.kernelgrok.com/)
* [GDB](http://users.ece.utexas.edu/~adnan/gdb-refcard.pdf)

## Challenges

*Most reversing challenges should be safe to run on your host, but it is always best to run on a virtual machine*

* [Crackmes.one](https://crackmes.one/)
* [OSX Crackmes](https://reverse.put.as/crackmes/)
* [ESET Challenges](http://www.joineset.com/jobs-analyst.html)
* [Flare-on Challenges](http://flare-on.com/)
* [Github CTF Archives](http://github.com/ctfs/)
* [Reverse Engineering Challenges](http://challenges.re/)
* [xorpd Advanced Assembly Exercises](http://www.xorpd.net/pages/xchg_rax/snip_00.html)
* [Malware-Traffic-Analysis](https://www.malware-traffic-analysis.net/)
* [Assembly Game](https://muchassemblyrequired.com/?utm_source=share&utm_medium=ios_app)
* [Nightmare Reversing](https://guyinatuxedo.github.io/)

## Virus Exchange

*Be careful with malware the below sites they host live malware*

* [VirusShare](http://virusshare.com/)
* [Contagio](http://contagiodump.blogspot.com/)
* [Malshare](http://malshare.com/)
* [VX Vault](http://vxvault.net/)
* [vx-underground](https://vx-underground.org/)
* [theZoo](https://thezoo.morirt.com/)

# Tools

## Virtual Machines

* [FLARE VM](https://github.com/fireeye/flare-vm)

## Binary Format

* [CFF Explorer](http://www.ntcore.com/exsuite.php)
* [PE-bear](https://hshrzd.wordpress.com/pe-bear/)
* [PEiD](https://tuts4you.com/download.php?view.398)
* [PPEE](https://www.mzrst.com/)
* [MachoView](https://github.com/gdbinit/MachOView)
* [nm](https://developer.apple.com/library/mac/documentation/Darwin/Reference/ManPages/man1/nm.1.html) 
* [file](https://developer.apple.com/library/mac/documentation/Darwin/Reference/ManPages/man1/file.1.html) 
* [codesign](https://developer.apple.com/library/mac/documentation/Darwin/Reference/ManPages/man1/codesign.1.html) 

## Disassemblers/Decompilers

* [Ghidra](https://ghidra-sre.org/)
* [IDA Free](https://www.hex-rays.com/products/ida/support/download_freeware.shtml)
* [Binary Ninja](https://binary.ninja/)
* [JEB](https://www.pnfsoftware.com/jeb2/)
* [Radare](http://www.radare.org/r/)
* [Hopper](http://hopperapp.com/)
* [Capstone](http://www.capstone-engine.org/)
* [objdump](http://linux.die.net/man/1/objdump)
* [fREedom](https://github.com/cseagle/fREedom)
* [Retdec](https://retdec.com/)
* [Snowman](https://derevenets.com/)

## Hex Editors

* [010 Editor](https://www.sweetscape.com/010editor/)

## Binary Analysis

* [Mobius Resources](http://www.msreverseengineering.com/research/)
* [z3](https://z3.codeplex.com/)
* [bap](https://github.com/BinaryAnalysisPlatform/bap)
* [angr](https://github.com/angr/angr)

## Bytecode Analysis

* [dnSpy](https://github.com/0xd4d/dnSpy)
* [Bytecode Viewer](https://bytecodeviewer.com/)
* [Bytecode Visualizer](http://www.drgarbage.com/bytecode-visualizer/)
* [JPEXS Flash Decompiler](https://www.free-decompiler.com/flash/)
* [uncompyle6](https://github.com/rocky/python-uncompyle6/)
* [JADX](https://github.com/skylot/jadx)

## Import Reconstruction

* [ImpRec](http://www.woodmann.com/collaborative/tools/index.php/ImpREC)
* [Scylla](https://github.com/NtQuery/Scylla)
* [LordPE](http://www.woodmann.com/collaborative/tools/images/Bin_LordPE_2010-6-29_3.9_LordPE_1.41_Deluxe_b.zip)

## Dynamic Analysis

* [ProcessHacker](http://processhacker.sourceforge.net/)
* [Process Explorer](https://technet.microsoft.com/en-us/sysinternals/processexplorer)
* [Process Monitor](https://technet.microsoft.com/en-us/sysinternals/processmonitor)
* [Autoruns](https://technet.microsoft.com/en-us/sysinternals/bb963902)
* [Noriben](https://github.com/Rurik/Noriben)
* [API Monitor](http://www.rohitab.com/apimonitor)
* [iNetSim](http://www.inetsim.org/)
* [Wireshark](https://www.wireshark.org/download.html)
* [Fakenet](http://practicalmalwareanalysis.com/fakenet/)
* [netzob](https://www.netzob.org/)
* [Volatility](https://github.com/volatilityfoundation/volatility)
* [Dumpit](http://www.moonsols.com/products/)
* [LiME](https://github.com/504ensicsLabs/LiME)
* [Cuckoo](https://www.cuckoosandbox.org/)
* [Objective-See Utilities](https://objective-see.com/products.html)
* [XCode Instruments](https://developer.apple.com/xcode/download/) - XCode Instruments for Monitoring Files and Processes [User Guide](https://developer.apple.com/library/watchos/documentation/DeveloperTools/Conceptual/InstrumentsUserGuide/index.html) 
* [dtrace](http://dtrace.org/blogs/brendan/2011/10/10/top-10-dtrace-scripts-for-mac-os-x/) - sudo dtruss = strace [dtrace recipes](http://mfukar.github.io/2014/03/19/dtrace.html)
* [fs_usage](https://developer.apple.com/library/mac/documentation/Darwin/Reference/ManPages/man1/fs_usage.1.html) - report system calls and page faults related to filesystem activity in real-time.  File I/O: fs_usage -w -f filesystem 
* [dmesg](https://developer.apple.com/library/mac/documentation/Darwin/Reference/ManPages/man8/dmesg.8.html) - display the system message buffer

## Debugging

* [WinDbg](https://msdn.microsoft.com/en-us/windows/hardware/hh852365.aspx)
* [OllyDbg v1.10](http://www.ollydbg.de/)
* [OllyDbg v2.01](http://www.ollydbg.de/version2.html)
* [OllySnD](https://tuts4you.com/download.php?view.2061)
* [Olly Shadow](https://tuts4you.com/download.php?view.6)
* [Olly CiMs](https://tuts4you.com/download.php?view.1206)
* [Olly UST_2bg](https://tuts4you.com/download.php?view.1206)
* [x64dbg](http://x64dbg.com/#start)
* [gdb](https://www.gnu.org/software/gdb/)
  * [gef](https://gef.readthedocs.io/en/master/)
* [vdb](https://github.com/vivisect/vivisect)
* [lldb](http://lldb.llvm.org/)
* [qira](http://qira.me/)
* [unicorn](https://github.com/unicorn-engine/unicorn)
