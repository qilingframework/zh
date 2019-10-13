<h1>What Is Missing</h1>
Insecure Internet of Things (IoT) and malware attack are affecting our day-to-day life. Hardware verdors and the entire security industry is struggling to fight againts the bad guys and at the same time trying to build a better product. Sadly, IoT threat analysis and malware analysis remain the two biggiest challanges in the security industry. 

Modern IoT threat and malware are moving towards different platform (Operating System) and CPU archirecture. Reverse engineers are not only struggling to understand diffrent operating systems and cpu architecture. Also, lacking of updated tools surely did not help. Tools available currently are not even any near to catch up with the speed of fast growing security threat.

Currently, available tools for doing analysis such as full system emulation, usermode emulation, binary instrumentation, disassembler and sandboxing are just barely enough. These tools are either limited in cross platform or multi CPU architecture support. These tools need to used seperately and analyzed data are not easy to compiled or cross referece. This also contribute to the reason why reverse enginnering is never a easy task.
 
---
<h1>Why Qiling Framework</h1>
Qiling Framework is aimed to change IoT security research, malware analysis and reverse engineering landscape. The main objective is to build a total solution for cross platform and cross architecture framework, not just another reverse enginnering tool. Qiling Framework is designed for easy to deploy, use and to build application on top of it. Qiling Framework is also fully open-source. Hence, sustainable future development could be benefited from the work of the community.

Qiling Framework is designed as a binary instrumentation and binary emulation framework that supports cross-platform and multi-architecture. It is also packed with powerful features such as code interception and arbitary code injection before or during a binary execution. It also able to patch a packed binary during execution.

Qiling Framework is able to runs on different operating system and supports different CPU architures. Qiling Framework is written in Python, a simple and commonly used programming language by reverse engineers.


---
<h1>Executive Summary</h1>
Qiling Framework is not yet another emulataion tool. It combines binary instrumentation and binary emulation into one single framework. With Qiling Framework, we can achieve

  - Redirect process execution flow on the fly
  - Hot-patching binary during execution
  - Code injection during execution
  - Partial binary execution, without running the entire file
  - Patch a "unpacked" content of a packed binary file

Qiling Framework emulates: 
  - Windows X86 32/64bit
  - Linux X86 32/64bit, ARM, AARCH64, MIPS
  - MacOS X86 32/64bit
  - FreeBSD X86 32/64bit

Qiling Framework is able to run on top of Windows/MacOS/Linux/FreeBSD without CPU architecture limitation

---

<h1>How does it work</h1>
##### Demo Setup
- *Hardware : X86 64bit*
- *OS : Ubuntu 18.04 64bit*

##### Demo #1 Catching Wannacry's killer switch
Qiling Framework executes Wannacry binary, hooking address 0x40819a to catch the killerswitch url

[![qiling DEMO 3: Catching wannacry's killer switch](https://img.youtube.com/vi/gVtpcXBxwE8/0.jpg)](https://www.youtube.com/watch?v=gVtpcXBxwE8 "Video DEMO 3")

###### Sample code

```python
from qiling import *

def stopatkillerswtich(ql):
    ql.uc.emu_stop()

if __name__ == "__main__":
    ql = Qiling(["rootfs/x86_windows/bin/wannacry.bin"], "rootfs/x86_windows")
    ql.hook_address(stopatkillerswtich, 0x40819a)
    ql.run()
```

###### Execution output

```
0x1333804: __set_app_type(0x2)
0x13337ce: __p__fmode() = 0x500007ec
0x13337c3: __p__commode() = 0x500007f0
0x132f1e1: _controlfp(0x10000, 0x30000) = 0x8001f
0x132d151: _initterm(0x40b00c, 0x40b010)
0x1333bc0: __getmainargs(0xffffdf9c, 0xffffdf8c, 0xffffdf98, 0x0, 0xffffdf90) = 0
0x132d151: _initterm(0x40b000, 0x40b008)
0x1001e10: GetStartupInfo(0xffffdfa0)
0x104d9f3: GetModuleHandleA(0x00) = 400000
0x125b18e: InternetOpenA(0x0, 0x1, 0x0, 0x0, 0x0)
0x126f0f1: InternetOpenUrlA(0x0, "http://www.iuqerfsodp9ifjaposdfjhgosurijfaewrwergwea.com", "", 0x0, 0x84000000, 0x0)
```
---

##### Demo #2 Hotpatching a Windows crackme
Using Qiling Framework to dynamically patch a Windows crackme binary so that it always displays "Congratulation" dialog

[![qiling DEMO 1: hotpatching a Windows crackme](http://img.youtube.com/vi/p17ONUbCnUU/0.jpg)](https://www.youtube.com/watch?v=p17ONUbCnUU "Video DEMO 1")

###### Sample code

```python
from qiling import *

def force_call_dialog_func(ql):
    # get DialogFunc address
    lpDialogFunc = ql.unpack32(ql.mem_read(ql.sp - 0x8, 4))
    # setup stack memory for DialogFunc
    ql.stack_push(0)
    ql.stack_push(1001)
    ql.stack_push(273)
    ql.stack_push(0)
    ql.stack_push(0x0401018)
    # force EIP to DialogFunc
    ql.pc = lpDialogFunc


def my_sandbox(path, rootfs):
    ql = Qiling(path, rootfs)
    # NOP out some code
    ql.patch(0x004010B5, b'\x90\x90')
    ql.patch(0x004010CD, b'\x90\x90')
    ql.patch(0x0040110B, b'\x90\x90')
    ql.patch(0x00401112, b'\x90\x90')
    # hook at an address with a callback
    ql.hook_address(0x00401016, force_call_dialog_func)
    ql.run()


if __name__ == "__main__":
    my_sandbox(["rootfs/x86_windows/bin/Easy_CrackMe.exe"], "rootfs/x86_windows")
```

###### Execution output

```
0x10cae10: GetStartupInfo(0xffffdf40)
0x1121fa7: GetStdHandle(0xfffffff6) = 0xfffffff6
0x111fbc4: GetFileType(0xfffffff6) = 0x2
0x1121fa7: GetStdHandle(0xfffffff5) = 0xfffffff5
0x111fbc4: GetFileType(0xfffffff5) = 0x2
0x1121fa7: GetStdHandle(0xfffffff4) = 0xfffffff4
0x111fbc4: GetFileType(0xfffffff4) = 0x2
0x1121fd1: SetHandleCount(0x20) = 32
0x1121fbf: GetCommandLineA() = 0x501091b8
0x111fcd4: GetEnvironmentStringsW() = 0x501091e4
0x1117ffa: WideCharToMultiByte(0x0, 0x0, 0x501091e4, 0x1, 0x0, 0x0, 0x0, 0x0) = 2
0x1117ffa: WideCharToMultiByte(0x0, 0x0, 0x501091e4, 0x1, 0x50002098, 0x2, 0x0, 0x0) = 1
0x111fcbc: FreeEnvironmentStringsW(0x501091e4) = 1
0x1116a0b: GetACP() = 437
0x1121f8f: GetCPInfo(0x1b5, 0xffffdf44) = 1
0x1121f8f: GetCPInfo(0x1b5, 0xffffdf1c) = 1
0x111e43e: GetStringTypeW(0x1, 0x40541c, 0x1, 0xffffd9d8) = 0
0x10ffc95: GetStringTypeExA(0x0, 0x1, 0x405418, 0x1, 0xffffd9d8) = 0
0x111e39c: LCMapStringW(0x0, 0x100, 0x40541c, 0x1, 0x0, 0x0) = 0
0x1128a50: LCMapStringA(0x0, 0x100, 0x405418, 0x1, 0x0, 0x0) = 0
0x111e39c: LCMapStringW(0x0, 0x100, 0x40541c, 0x1, 0x0, 0x0) = 0
0x1128a50: LCMapStringA(0x0, 0x100, 0x405418, 0x1, 0x0, 0x0) = 0
0x111685a: GetModuleFileNameA(0x0, 0x40856c, 0x104) = 42
0x10cae10: GetStartupInfo(0xffffdfa0)
0x11169f3: GetModuleHandleA(0x00) = 400000
0x104cf42: DialogBoxParamA(0x400000, 0x65, 0x00, 0x401020, 0x00) = 0
Input DlgItemText :

        << enter any string or number here >>

0x1063d14: GetDlgItemTextA(0x00, 0x3e8, 0xffffdef4, 0x64) = 3
0x105ea11: MessageBoxA(0x00, "Congratulation !!", "EasyCrackMe", 0x40) = 2
0x1033ba3: EndDialog(0x00, 0x00) = 1
0x1124d12: ExitProcess(0x01)
```
