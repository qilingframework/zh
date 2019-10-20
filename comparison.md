---
layout: page
title: qiling框架与其他开源模拟器和工具的比较
permalink: /comparison/
---

目前有许多开源模拟器，但有两个项目最接近Qiling框架是[Unicorn](http://www.unicorn-engine.org)和[Qemu usermode](https://qemu.org)。本节总结了Qiling与它们的主要区别。

#### Qiling Framework vs Unicorn Engine
Qiling框架建立在Unicorn之上。然而，Qiling和Unicorn是不同的。

Unicorn只是一个CPU模拟器。因此，它侧重于模拟CPU指令，并且可以操作内存空间。除此之外，Unicorn不支持更高层次的概念，比如动态库、系统调用、I/O处理或可执行文件格式，比如PE、MachO或ELF。简而言之，Unicorn只模拟原始汇编指令，而不模拟操作系统（OS）上下文

Qiling被设计为一个更高级别的框架，它利用Unicorn来模拟CPU指令，但Qiling理解OS：它有可执行文件加载功能（目前用于PE、MachO和ELF）、动态链接程序（以便我们可以加载和重定位共享库）、Syscall和IO处理功能。因此，Qiling可以运行通常可以在操作系统中运行的可执行二进制文件。

#### Qiling Framework vs Qemu usermode
Qemu用户模式也做了类似的事情，即以跨体系结构的方式模拟执行整个可执行二进制文件。然而，与Qemu用户模式相比，Qiling提供了一些重要的区别。

Qiling是一个真正的分析框架，它允许您在上面构建自己的动态分析工具（使用友好的Python语言）。同时，Qemu只是一个工具，而不是一个框架

Qiling可以执行动态检测，甚至可以在运行时修补代码。Qemu也不支持这样的功能

Qiling不仅是跨架构的，而且是跨平台的。例如，您可以在Windows上运行Linux ELF文件。Qemu usermode只运行相同操作系统的二进制文件，例如Linux主机上的Linux ELF，这是因为它将系统调用从模拟代码转发到本机操作系统的方式。

Qiling支持更多平台，包括Windows、MacOS、Linux和BSD。Qemu用户模式只处理Linux和BSD

#### Qiling Framework vs Qemu
不会翻译

#### Qiling Framework vs Usercorn
Usercorn是带有插桩功能的仿真工具，类似于Qiling Framework的功能，它能够进行系统调用转发，插桩

但是，Usercorn仅支持Linux（一定程度上支持MacOS）。Qiling Framework在平台和体系结构上支持更全面

#### Qiling Framework vs Binee
Binee是一个用Go语言开发的仿真工具，但它不是一个框架。Binee不允许动态hook、热修补或提供任何自定义功能。作为Python模块设计的Qiling框架提供了更多的功能，使得很多动态分析成为可能

Binee只支持windows。Qiling框架支持更多平台和架构

#### Qiling Framework vs Wine
Wine是一个模拟工具，不是用来分析的框架。它只在Linux、Mac、Freebsd和Solaris上模拟Windows，允许用户在*nix平台上运行Windows应用程序

Qiling框架并不是为此目的而构建的, 虽然Qiling可以运行许多其他平台和体系结构运行应用程序，但Qiling是用来做安全分析的

#### Qiling Framework vs Cuckoo Sandbox
Cuckoo Sandbox是一个基于虚拟机的分析工具，即qemu、virtualbox，为二进制执行提供虚拟化环境。

Qiling framework在没有运行完整操作系统的情况下执行二进制文件。它理解操作系统并将系统调用从模拟代码本地转发到操作系统
