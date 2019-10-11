---
layout: page
title: Qiling Framework vs other open source emulators and tools
permalink: /comparison/
---

There are many open source emulators, but two projects closest to Qiling are [Unicorn](http://www.unicorn-engine.org) & [Qemu usermode](https://qemu.org). This section summaries the main differences.

##### Qiling Framework vs Unicorn engine

Qiling Framework is built on top of Unicorn. However, Qiling and Unicorn are two different beasts

- Unicorn is just a CPU emulator. Hence, it focuses on emulating CPU instructions, that can understand emulator memory. Beyond that, Unicorn is not aware of higher level concepts, such as dynamic libraries, system calls, I/O handling or executable formats like PE, MachO or ELF. In short, Unicorn only emulates raw machine instructions, without Operating System (OS) context
- Qiling is designed as a higher level framework, that leverages Unicorn to emulate CPU instructions, but Qiling understands OS: it has executable format loaders (for PE, MachO & ELF at the moment), dynamic linkers (so we can load & relocate shared libraries), syscall & IO handlers. For this reason, Qiling can run excutable binaries that normally runs in native OS

##### Qiling Framework vs Qemu usermode

Qemu usermode does similar thing, that is to emulate whole executable binaries in cross-architecture way. However, Qiling offers some important differences bewteen Qemu usermode

- Qiling Framework is a true analysis framework, that allows you to build your own dynamic analysis tools on top (in friendly Python language). Meanwhile, Qemu is just a tool, not a framework
- Qiling Framework can perform dynamic instrumentation, and can even hotpatch code at runtime. Qemu does not do either
- Not only working cross-architecture, Qiling is also cross-platform. For example, you can run Linux ELF file on top of Windows In contrast, Qemu usermode only run binary of the same OS, such as Linux ELF on Linux host, due to the way it forwards syscall from emulated code to native OS
- Qiling Framework supports more platforms, including Windows, MacOS, Linux & BSD. Qemu usermode only handles Linux & BSD

##### Qiling Framework vs Qemu
- Qemu is a full system emulator, but not an analysis tool. Qemu comes with build-in GDB and we cannot analyze a process via qemu. In contrast, Qiling Framework does not perform full system emulation but it still understands OS, syscalls & IO handlers.

##### Qiling Framework vs Usercorn
- [Usercorn](https://usercorn.party) is an emulation tool with instrumentation, which is similar to Qiling Framework's capability where it is able to perform syscall forwarding, instrumentation
- However, Usercorn only supports Linux (and MacOS, to some extent). Qiling Framework, on the other hand, has vast support on platforms and architecture

##### Qiling Framework vs Binee
- Binee is an emulation tool built with GO language but it is not an instrumentation framework. Binee does not allow dynamic hooking, hotpatching or provide any customization. Qiling Framework, designed as a Python module, offers far more capability, making a lot of dynamic analysis possible
- Binee supports only Windows. Qiling Framework supports more platforms and architecture

##### Qiling Framework vs Wine
- Wine is an emulation tool not intended for analysis purpose. It only emulates Windows on Linux, Mac, FreeBSD, and Solaris, allowing user to run Windows applications on *NIX platforms
- Qiling Framework is not built for this purpose, although it is possible to run applications from many other platforms and archirectures. Qiling is meant for security analysis

##### Qiling Framework vs Cuckoo Sandbox
- Cuckoo Sandbox is an analysis tool relying on VM i.e. QEMU, Virtualbox to provide virtualized environment for binary execution
- Qiling Framework executes binary without having full blown OS running. It understands OS and forwards syscalls from emulated code to OS natively
