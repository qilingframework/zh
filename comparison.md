---
layout: page
title: 麒麟框架与其他开源模拟器和工具的比较
permalink: /comparison/
---

目前有许多开源模拟器，但有两个项目最接近麒麟框架是[Unicorn](http://www.unicorn-engine.org)和[Qemu usermode](https://qemu.org)。本节总结了麒麟框架与它们的主要区别。

##### 麒麟框架 vs Unicorn Engine
麒麟框架基于Unicorn开发。然而二者是有区别的。

  - Unicorn只是一个CPU模拟器，侧重于模拟CPU指令与操作内存。此外，Unicorn不支持高阶操作，比如动态库、系统调用、I/O处理或可执行文件格式（PE、MachO或ELF等）。因此，Unicorn只模拟最原始的汇编指令，而无法模拟模拟操作系统。

  - 麒麟框架则是一个更高阶的框架，它利用Unicorn来模拟CPU指令，并且麒麟框架有可执行文件加载功能（目前用于PE、MachO和ELF）、动态链接程序（以便我们可以加载和重定位共享库）、Syscall和IO处理功能。因此，麒麟框架可以运行各类二进制文件。

---

##### 麒麟框架 vs Qemu usermode
Qemu usermode也可以用跨体系结构的方式模拟执行二进制文件。然而：

  - 麒麟框架是一个真正的分析框架，你能以它为基础构建自己独特的动态分析工具（使用Python语言）。但是，Qemu usermode只是一个工具，而不是一个框架。

  - 麒麟框架可以执行动态检测，甚至可以在运行的同时修补代码。Qemu用户模式则不支持。

  - 麒麟框架不但跨架构，而且是跨平台的（例如，您可以在Windows上运行Linux ELF文件）。而Qemu usermode却只能运行相同操作系统的二进制文件（例如，Linux主机上的Linux ELF），这是因为它将系统调用从模拟代码转发到本机操作系统的方式。

  - 麒麟框架支持更多平台，包括Windows、MacOS、Linux和BSD。Qemu usermode只处理Linux和BSD。

---

##### 麒麟框架 vs Qemu
Qemu是一个完整的系统模拟器，但它不是分析工具。 Qemu带有内置的GDB，但是我们无法通过Qemu分析流程。 相比之下，麒麟框架虽然不会模拟完整的系统，但可以进行系统调用、处理IO程序。

---

##### 麒麟框架 vs Usercorn
  - Usercorn是带有插桩功能的模拟器，这和麒麟框架有些类似。

  - 但是，Usercorn只支持Linux（一定程度上也支持MacOS），麒麟框架则支持更多的操作系统。

---

##### 麒麟框架 vs Binee
  - Binee是一个用Go语言开发的模拟器具，但它仍然不是一个框架。Binee不允许动态hook、热修补，且没有任何自定义的功能。而使用Python语言设计的麒麟框架，则提供了更多的功能，并且可以进行动态分析。

  - Binee只支持Windows，麒麟框架则支持更多的操作系统。
  
---

##### 麒麟框架 vs Wine
  - Wine是一个模拟器，不是用来分析的框架。它只在Linux、Mac、Freebsd和Solaris上模拟Windows，允许用户在\*NIX平台上运行Windows应用程序

  - 麒麟框架则不同，它不但可以模拟的系统与架构并运行应用程序，最关键的是，麒麟框架是用来做安全分析的。

---

##### 麒麟框架 vs Cuckoo Sandbox
Cuckoo Sandbox是一个基于虚拟机的分析工具，即qemu、virtualbox，为二进制执行提供虚拟化环境。

麒麟框架则可以在没有运行完整操作系统的情况下执行二进制文件，并且它可以和宿主OS更完美的对接。
