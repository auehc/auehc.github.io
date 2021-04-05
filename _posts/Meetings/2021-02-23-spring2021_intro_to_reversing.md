---
title:  "Introduction to Reverse Engineering Spring 2021"
permalink: /meetings/Intro_to_Reversing_Spring_2021
tags: meetings
author: therealjman
---

For the next few weeks, we plan to cover reverse engineering. However, in order to do so, we need to give some background to why reverse engineering is important, and how to analyze assembly languages. We will start off this week with a discussion of the x86 architecture and the IA-32 assembly language.

# Topics

## What is Reversing?

Software reverse engineering, commonly referred to as reverse engineering or just reversing, is the process of taking software apart and analyzing it. When the source code is not available for a particular piece of software, it is referred to as binary reverse engineering. This process can be very frustrating and difficult at times, however reversing a piece of software is often like a puzzle, where you try to piece together what it does and how it works. There are some skills that are useful to have when performing reversing, such as familiarity with an assembly languages, strong knowledge of compiled programming languages, and most importantly, the ability to learn (and Google search well).

## Why do Reversing?

One of the most common uses for reversing skills is malware analysis. Computer malware has already caused trillions of dollars worth of damages in the past few years and is projected to cause a lot more in the upcoming years. Each major operating system has its own format for executables. Windows has the portable executable (PE) format, Linux has the Executable and Linkable Format (ELF), and macOS has Mach-O. In our discussions on reversing, we will be primarily focusing on the PE format, with some discussion on ELF.

## Background Information

### Binary Files

Programs are usually generated into binary files, which are computer readable files stored in the binary number format. (For more information about binary and other number formats, you can look at our writeup for the disk forensics lecture from earlier in the semester.) Programming languages are compiled to bytecode which then is interpreted by a program and converted to machine instructions for the CPU. However, one thing to keep in mind is that not all binary files are executables, as things like JPG or PNG images are also binary files.

### C/C++ Compilation Process

The process for compiling C or C++ code into executable machine code has multiple steps. First, the preprocessor expands directives, which encompasses file inclusions and macros and then replaces all of the code comments with whitespace. Then the compiler translates the source code into assembly code and performs some optimization on it. Next, the assembler translates the assembly into machine code, adding relevant information for the binary format. Finally, the linker resolves all external library calls and produces the final executable.

### Linking Types

There are three main types of linking: static, dynamic, and runtime linking. Static linking is when libraries are copied into the final binary. This leads to a larger executable and makes it much harder to determine what functions come from libraries and which ones were written by the programmer. Dynamic linking is when the host OS searches for libraries when the program is loaded into memory. This is a fairly common method of linking that leads to smaller files than static linking and it is much easier to see what functions were imported. Finally, runtime linking only pulls the function when it is needed while the program is executing. This is somewhat rare and is usually performed by malicious code trying to obscure its functionality.

## IA-32 Assembly Crash Course

### The x86 Assembly Language

The x86 assembly language is a family of languages that was originally developed for Intel processors but was eventually able to run on AMD processes as well. There are two common versions of it. IA-32 (or i386) is the 16-bit version of the language, and x86-64 (or just x64) is the 64-bit version of the language. Knowledge of some important data sizes is crucial for understanding assembly, and the most common sizes are as follows:

* **Byte:** 8 bits
* **Word:** 16 bits or 2 bytes
* **Double Word (DWORD):** 32 bits or 4 bytes
* **Quadruple Word (QWORD):** 64 bits or 8 bytes

There are also a few primitive data types in x86 that are useful to know.

* **Character:** A single ASCII character with a size of 1 bytes.
* **Integer:** Either a signed or unsigned whole number with a size of 4 bytes.
* **Float:** Either a signed or unsigned decimal number with a size of 8 bytes.

### Registers and Memory

Registers are small units of storage contained within the central processing unit (CPU). The x86 architecture has 8 general-purpose registers, 6 segment registers, 1 flags register (EFLAGS) and an instruction pointer register (EFLAGS). Each general purpose register has at most 32 bits, but they can also be referenced by their 16-bit registers. Flags are very important for program flow, and there are three common ones to keep track of.

* **ZF (Zero Flag):** This flag is set when the result of an operation is zero and is cleared otherwise.
* **CF (Carry Flag):** This flag is set when the result of an operation is too large or small for the destination operand, and cleared otherwise.
* **SF (Sign Flag):** This flag is set when the result of an operation is negative, and is cleared when the result is positive.

Memory for a program can be divided into four major sections, the code, stack, heap, and data. The code section consists of all the executable instructions. The stack contains local variables and parameters for functions. The heap contains dynamic memory and the data section contains global and static variables. A full list of x86 registers and flags can be found [here](https://en.wikibooks.org/wiki/X86_Assembly/X86_Architecture).

### Calling Conventions and Instruction Format

Calling conventions are how functions handle receiving parameters and how to return their results. This can vary by architecture and compiler, and some compilers even support multiple calling conventions. There are three main calling conventions, listed below.

* **cdecl** - This is usually the default calling convention. Parameters are passed via the stack, stack cleanup is handled by the caller, and the return address is stored in EAX,
* **fastcall** - Parameters are passed via the ECX and EDX registers, stack cleanup is handled by the callee, and the return address is stored in EAX.
* **stdcall** - This is the standard calling convention for Microsoft's Win32 API. Parameters are passed via the stack, stack cleanup is handled by the callee, and the return address is stored in EAX.

Instructions in IA-32 assembly follow a certain format: ```mnemonic op1, op2, op3, ..., opN```. The mnemonic is also referred to as the instruction, and this is used to determine what each instruction is. The op1 - opN are operands passed to the instruction, and the exact number of them can vary per instruction.

### Intel vs. AT&T Format

There are two main syntaxes for x86 assembly, Intel and AT&T. The Intel syntax is used by Windows and places the destination register before the source. Operand size is derived from the name of the register and the assembler automatically detects the type of the operands. The AT&T syntax is primarily used by macOS and Linux and places the destination after the source. Instead of the register name, mnemonics denote operand size and immediate values are prefixed with ```$``` and registers are prefixed with ```%```. The Intel syntax is the more popular of the two and is what we will be discussing in this article.

## Common Instructions

There are many different instructions in IA-32 assembly, and while learning every single one is difficult it is useful to familiarize yourself with some of the most common instructions. Below is a list of some of the most common IA-32 instructions with their syntax and a short description of what each one does.

* **mov (Move)** - Syntax: ```mov destination, source``` - Moves data from the *source* register to the *destination* register. This instruction can also be used to dereference pointers using the ```[ ]``` syntax around either the destination or source operand.

* **lea (Load Effective Address)** - Syntax: ```lea, destination, [source]``` - Load effective address from *source* into *destination*. This is used to get the address of the variable in source and can also be used to perform quick arithmetic.

* **add (Add)** - Syntax: ```add destination, source``` - Adds *source* to *destination* and stores the result in *destination*.

* **sub (Subtract)** - Syntax: ```sub destination, source``` - Subtracts *source* from *destination* and stores the result in *destination*.

* **inc (Increment)** - Syntax: ```inc register``` - Increments *register* by one and stores the result back into *register*.

* **dec (Decrement)** - Syntax: ```dec register``` - Decrements *register* by one and stores the result back into *register*.

* **shl (Shift Logical Left)** - Syntax: ```shl source, value``` - Bit shifts *source* to the left by *value*. For information on the difference between logical and arithmetic shifts, check out [this](https://open4tech.com/logical-vs-arithmetic-shift/) article.

* **sal (Arithmetic Shift Left)** - Syntax: ```sal source, value``` - Arithmetic shifts *source* to the left by *value*. Shift left is typically used to multiply values by powers of two.

* **shr (Shift Logical Right)** - Syntax: ```shr source, value``` - Bit shifts *source* to the right by *value*.

* **sar (Arithmetic Shift Right)** - Syntax: ```sar source, value``` - Arithmetic shifts *source* to the right by *value*. Shift right is typically used to divide values by powers of two.

* **mul (Unsigned Multiply)** - Syntax: ```mul value``` - Multiplies *value* by *EAX* and stores into *EDX* and *EAX*.

* **imul (Signed Multiply)** - Syntax: ```imul value``` or ```imul destination, source``` - Multiplies *value* by *EAX* and stores into *EDX* and *EAX*, preserving the sign of the result. The alternate syntax multiplies *destination* by *source* and stores into *destination*.

* **div (Unsigned Division)** - Syntax: ```div value``` - Divides *value* by *EDX:EAX* and stores remainder into *EDX* and value into *EAX*.

* **idiv (Signed Division)** - Syntax: ```idiv value``` - Divides *value* by *EDX:EAX* and stores remainder into *EDX* and value into *EAX*, preserving the sign of the result.

* **Size Directives** - Typically, the size of a data item can be inferred by what instruction it is being used in, but sometimes it can be ambiguous. One way to fix this is to use directives, which explicitly specify the size of an operand. An example of this is ```mov WORD PTR [eax], 8```, which moves the 2-byte representation of 8 into the 2 bytes at the address in EAX.

## Logical Operands

In addition to these common instructions, the IA-32 language has quite a few logical operations. A list of some of the common ones is below. For clarification on some of the bitwise operations, the [Wikipedia](https://en.wikipedia.org/wiki/Bitwise_operation) page on them does a good job of explaining them.

* **and (Logical AND)** - Syntax: ```and destination, source``` - Performs a bitwise and on *destination* and *source* and stores result in *destination*.

* **or (Logical OR)** - Syntax: ```or destination, source``` - Performs a bitwise or on *destination* and *source* and stores result in *destination*.

* **xor (Logical XOR)** - Syntax: ```xor destination, source``` - Performs a bitwise xor on *destination* and *source* and stores result in *destination*.

* **not (Bitwise Negation)** - Syntax: ```not destination``` - Performs a bitwise negation on *destination* and stores in *destination*.

* **neg (Two's Complement Negation)** - Syntax: ```neg destination``` - Replaces value in *destination* with the two's complement value. Two's complement is a way of storing negative numbers in a binary format. For more information on it check out [this webpage](https://www.cs.cornell.edu/~tomf/notes/cps104/twoscomp.html) from Cornell.

## Control Flow

Labels are used to refer to a labeled location in the program code, the most common use for them is labeling function locations. They can be added anywhere by using the syntax ```<label>:```. In addition to labels, there are also some instructions that help dictate program flow and many of these use the flags discussed earlier in the article. Some of the more common instructions are listed below.

* **cmp (Compare)** - Syntax: ```cmp destination, source``` - Compares *destination* against *source* by subtracting *source* from *destination*. The result of the subtraction is not stored, it is only used to set certain flags. This instruction is commonly used right before a conditional jump instruction to perform the comparison for the branch.

* **test (Test)** - Syntax: ```test destination, source``` - Tests *destination* against *source* by and'ing *source* against *destination*. Once again, the result of this is only used to set flags and is not stored. This instruction is usually used with the same *source* and *destination* registers to check if a value is zero.

* **jmp (Jump)** - Syntax: ```jmp address``` or ```jmp label``` - Performs an unconditional jump to *address* or *label*.

* **jz (Jump if Zero)** - Syntax: ```jz address``` or ```jz label``` - Jumps to *address* or *label* if the prior instruction set the zero flag (ZF).

* **jnz (Jump if not Zero)** - Syntax: ```jnz address``` or ```jnz label``` - Jumps to *address* or *label* if the prior instruction did not set ZF.

* **jl (Jump if Less)** - Syntax: ```jl address``` or ```jl label``` - Jumps to *address* or *label* if the prior comparison is less.

* **jg (Jump if Greater)** - Syntax: ```jg address``` or ```jg label``` - Jumps to *address* or *label* if the prior comparison is greater.

* **call (Call)** - Syntax: ```call address``` or ```call label``` - Changes the execution flow to the *address* or *label* specified. This works by pushing EIP to the stack and then setting EIP to the new *address*.

* **ret (Return)** - Syntax: ```ret``` - Returns from the current function and resumes execution from before the function call. This instruction pulls the EIP off of the stack and resumes from the address stored in it.

## Stack and Heap

The stack is a portion of memory primarily used for local variables and function parameters. There are two registers that are responsible for keeping track of the beginning and end of the stack: EBP and ESP. EBP is the base of the stack and ESP is the base of the stack. The stack is a last in first out data structure with a head down orientation, meaning it grows downward to lower memory addresses. There are two important instructions for the stack: ```push EAX```, which subtracts ESP by a dword and pushes the value in *EAX* to the stack and ```pop EAX```, which stores the content of ESP in *EAX* and adds a dword to ESP to push the stack pointer back up. The heap is a data structure that is used for dynamic memory, however it is incredibly complicated so an in-depth discussion of it is outside the scope of this article.

### Stack Prologue/Epilogue

When entering and leaving functions, the compiler usually inserts code to properly create and destroy the stack frame. This code is called the stack prologue or stack epilogue. However, this is not guaranteed, as sometimes compilers can skip this step. The most common way to see a stack prologue is with the following set of instructions:

```
push ebp
mov ebp, esp
sub esp, N
```

Then the stack epilogue is typically the following three instructions:

```
mov esp, ebp
pop ebp
ret
```

## Data Structures

The IA-32 language supports all of the same data structures that high-level programming languages do like loops, arrays, and function calls. However, these structures usually take multiple instructions to implement in assembly. For an example, a single ```if``` statement in C might be implemented with a ```cmp``` and conditional jump instruction in IA-32. For some specific examples of how some of these data structures are implemented in IA-32, there are some examples at the end of the slide deck for this week.

# Slideshow

<iframe src="//docs.google.com/gview?url=http://auehc.github.io/assets/powerpoints/Intro_to_Reversing_Spring2021.pptx&embedded=true" style="width:600px; height:500px;" frameborder="0"></iframe>
