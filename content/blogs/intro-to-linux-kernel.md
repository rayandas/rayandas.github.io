+++
date = '2020-03-27T14:52:58+05:30'
draft = false
title = 'Intro to Linux Kernel'
+++
As we all know, Linux is a member of the large family of Unix-like operating systems. Linux was initially developed by Linus Torvalds as an operating system. Linus remains deeply involved with improving Linux, keeping it up-to-date with various hardware developments, and coordinating the activity of hundreds of Linux developers around the world.

One of the benefits of Linux is that it isn't commercial operating system, it's source code under the GNU license is open and available to anyone to use and contribute.

### Basic Operating System Concepts.
Each computer system includes the basic set of programs called the operating system. The most important program in the set is called the kernel. It is loaded into RAM when the system boots and contains many critical procedures that are needed for the system to operate. The kernel provides key facilities to everything else on the system and determines many of the characteristics of higher software.
The operating system must fulfill two main objectives:
* Interact with the hardware components, servicing all low-level programmable elements included in the hardware platform.
* Provide an execution environment to the applications that run on the computer system.

Some operating system allows all user programs to directly play with the hardware components(like MS-DOS). A Unix-like operating system hides all low-level details concerning the physical organization of the computer from applications runs by the user. When a program wants to use use a hardware resource, it must issue a request to the operating system. The kernel evaluates the request and, if it chooses to grant the request the resource, interacts with the proper hardware components on behalf of the user program.

### Kernel Architecture
Most Unix kernels are monolithic: each kernel layer is integrated into the whole kernel program and runs in Kernel Mode on behalf of the current process. In contrast, microkernel operating systems demand a very small set of functions from the kernel, generally including a few synchronization primitives, a simple scheduler, and an interprocess communication mechanism.

Microkernels are generally slower than monolithic operating systems. However, microkernel operating systems might have a theoretical advantages over monolithic ones. Microkernels force the system programmers to adopt a modularized approach, because each operating system layer is a relatively independent program that must interact with the other layers through well defined and clean software interfaces.

To achieve many of the theoretical advantages of microkernels without introducing performance penalties, the Linux kernel offers modules. A module is an object file whose code can be link to (and unlink from) the kernel at runtime.

The main advantage of using modules include:

#### A modularized approach:
Because any module can be linked and unlinked at runtime, system programmers must introduce well-defined software interfaces to access the data structures handled by modules. This makes it easy to develop new modules.

#### Platform independence:
It may rely on some specific hardware features, but a module doesn't depend on a fixed hardware platform.

#### Frugal main memory usages:
A module can be linked to the running kernel when its functionality is required and unlinked when it is no longer useful.

#### No performance penalty:
Once linked in, the object code of a module is equivalent to the object code of the statically linked kernel. Therefore, no explicit message passing is required when the functions of the modules are invoked.

