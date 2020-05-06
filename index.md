<h1>二进制分析工具的现状</h1>
物联网设备正面临前所未有的威胁。恶意软件攻击的对象通常是安全性差或者配置不当的网络设备。硬件厂商和安全行业都在努力研究各种攻击行为，以制造更安全的产品。而“针对物联网设备的攻击”和“恶意软件分析”则是这个过程中，我们所面临的两个最大的挑战。

目前“物联网设备”和“恶意软件”同时运行于各种不同的操作系统与CPU架构中，逆向工程师需要了解全部CPU架构，这极大的降低了分析效率。同时，很多无法得到及时更新的分析工具，在面对层出不穷的新型攻击方式时，则显得捉襟见肘。

而现阶段很多二进制分析工具（系统仿真、用户模式仿真、二进制插桩工具和沙箱）， 都只针对单一类型的操作系统或CPU架构，且这些工具间几乎不可能共享信息或交叉引用数据。 这就是逆向工程的困难所在。

[1]Sonicwall的研究显示，2018年，恶意软件攻击大幅上升，达到105.2亿次，创下历史新高，且网络犯罪分子使用了新的威胁策略。

---
<h1>解决方案</h1>
麒麟框架旨在改变物联网安全研究、恶意软件分析和逆向工程的现状。我们的目标是构建一个跨平台、支持多体系结构的分析框架，而不仅仅是做一个逆向工具。麒麟框架拥有强大的功能，例如在二进制执行之前或执行期间进行代码拦截和任意代码注入。它还可以在执行期间补丁目标二进制文件。

麒麟框架是用Python编写的开源工具。Python是逆向工程师常用的简单的编程语言，这极大的降低了二次开发的门槛。

---
<h1>麒麟框架是什么</h1>
麒麟框架不仅仅是一个仿真平台或逆向工程工具。它还将“二进制插桩”和“二进制仿真”结合一起。借助麒麟框架，你可以：
  - 动态干预二进制程序执行流程
  - 在二进制程序执行期间对其进行动态补丁
  - 在二进制程序执行期间对其进行代码注入
  - 局部执行二进制程序，而不是运行整个文件
  - 任意补丁“脱壳”已加壳程序内容

麒麟框架能够模拟：
  - Windows x86 32/64位
  - Linux x86 32/64位，ARM，AARCH64，MIPS
  - MacOS x86 32/64位
  - FreeBSD x86 32/64位
  - UEFI

麒麟框架能够在Linux/MacOS/FreeBSD/Windows(WSL)等操作系统上运行，且不受CPU架构的限制

---

<h1>麒麟框架是如何操作的</h1>
##### 演示环境
- *Hardware : X86 64位*
- *OS : Ubuntu 18.04 64位*

##### 演示#1 如何用IDAPro和麒麟框架解简单的CTF题目
用IDAPro和麒麟框架解简单的CTF题目

[<img src="https://raw.githubusercontent.com/qilingframework/zh/master/images/demo1.jpg" width="500">](https://www.bilibili.com/video/av93142763 "演示#1 如何用IDAPro和麒麟框架解简单的CTF题目")

---
##### 演示#2 获取Wannacry的断路器开关地址
麒麟框架运行Wannacry恶意软件获取断路器开关地址

[<img src="https://raw.githubusercontent.com/qilingframework/zh/master/images/demo2.jpg" width="500">](https://www.bilibili.com/video/av73975753 "演示#2 获取Wannacry的断路器开关地址")

###### 代码样本

```python
from qiling import *

def stopatkillerswtich(ql):
    ql.uc.emu_stop()

if __name__ == "__main__":
    ql = Qiling(["rootfs/x86_windows/bin/wannacry.bin"], "rootfs/x86_windows")
    ql.hook_address(stopatkillerswtich, 0x40819a)
    ql.run()
```

###### 执行输出

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
##### 演示#3 在Ubuntu X64位上模拟ARM路由器固件
麒麟框架动态补丁及模拟ARM路由器固件，把其/usr/bin/httpd在X86_64位 Ubuntu上运行

[<img src="https://raw.githubusercontent.com/qilingframework/zh/master/images/demo3.jpg" width="500">](https://www.bilibili.com/video/av65935353 "演示#3 在Ubuntu X64位上模拟ARM路由器固件")

###### 代码样本

```python
from qiling import *

def my_sandbox(path, rootfs):
    ql = Qiling(path, rootfs, stdin = sys.stdin, stdout = sys.stdout, stderr = sys.stderr)
    # Patch 0x00005930 from br0 to ens33
    ql.patch(0x00005930, b'ens33\x00', file_name = b'libChipApi.so')
    ql.root = False
    ql.run()


if __name__ == "__main__":
    my_sandbox(["rootfs/tendaac15/bin/httpd"], "rootfs/tendaac15")
```
---
##### 演示#4 模拟UEFI
麒麟框架模拟UEFI

[![演示#4: 模拟UEFI](https://raw.githubusercontent.com/qilingframework/qilingframework.github.io/master/images/demo4-s.png)](https://raw.githubusercontent.com/qilingframework/qilingframework.github.io/master/images/demo4-en.png "演示#4: 模拟UEFI")

###### 代码样本
```python
import sys
import pickle
sys.path.append("..")
from qiling import *

def force_notify_RegisterProtocolNotify(ql, address, params):
    event_id = params['Event']
    if event_id in ql.loader.events:
        ql.loader.events[event_id]['Guid'] = params["Protocol"]
        # let's force notify
        event = ql.loader.events[event_id]
        event["Set"] = True
        ql.loader.notify_list.append((event_id, event['NotifyFunction'], event['NotifyContext']))
        ######
        return ql.os.ctx.EFI_SUCCESS
    return ql.os.ctx.EFI_INVALID_PARAMETER


if __name__ == "__main__":
    with open("rootfs/x8664_efi/rom2_nvar.pickel", 'rb') as f:
        env = pickle.load(f)
    ql = Qiling(["rootfs/x8664_efi/bin/TcgPlatformSetupPolicy"], "rootfs/x8664_efi", env=env)
    ql.set_api("hook_RegisterProtocolNotify", force_notify_RegisterProtocolNotify)
    ql.run()
```
