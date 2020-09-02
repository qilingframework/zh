麒麟框架是一个超轻量级的“沙盒”，适用于Linux、MacOS、Windows、FreeBSD、DOS、UEFI和MBR。它支持x86（16、32和64位）、ARM、ARM64和MIPS。

二进制检测和API是麒麟框架的主要及优先关注点。它是为逆向工程师设计的，因此省略搭建另一个沙盒工具的需求。使用麒麟框架可以节省时间。API丰富的麒麟框架将逆向工程及二进制代码检测快速的提升到了一个新的层次。

此外，麒麟框架还提供了对寄存器、内存、文件系统、操作系统和调试器的API访问。麒麟框架也提供了虚拟机级别的API，如保存和恢复执行状态。

麒麟框架也在各大国际安全峰会亮相
- 2020年:
    - [Black Hat, 美国](https://www.blackhat.com/us-20/arsenal/schedule/index.html#qiling-framework-from-dark-to-dawn-----enlightening-the-analysis-of-the-most-mysterious-iot-firmware--21062)
    - [Black Hat, 亚洲](https://www.blackhat.com/asia-20/arsenal/schedule/index.html#qiling-lightweight-advanced-binary-analyzer-19245)
    - [Hack In The Box, Lockdown 001](https://conference.hitb.org/lockdown-livestream/)
    - [Hack In The Box, Lockdown 002](https://conference.hitb.org/hitb-lockdown002/virtual-labs/virtual-lab-qiling-framework-learn-how-to-build-a-fuzzer-based-on-a-1day-bug/)
    - [Nullcon](https://nullcon.net/website/goa-2020/speakers/kaijern-lau.php)
    
- 2019年:
    - [Defcon, 美国](https://www.defcon.org/html/defcon-27/dc-27-demolabs.html#QiLing)
    - [Hitcon](https://hitcon.org/2019/CMT/agenda)
    - [Zeronights](https://zeronights.ru/report-en/qiling-io-advanced-binary-emulation-framework/)

---
<h1>为什么我们需要麒麟框架</h1>
智能互联网连接或所谓的“物联网”设备的不安全性比以往任何时候都更加令人担忧。恶意软件攻击的对象通常是安全性差或者配置不当的网络设备。硬件厂商和安全行业都在努力研究各种攻击行为，以制造更安全的产品。而“针对物联网设备的攻击”和“恶意软件分析”则是这个过程中，我们所面临的两个最大的挑战。

目前“物联网设备”和“恶意软件”同时运行于各种不同的操作系统与CPU架构中，逆向工程师需要了解全部CPU架构，这极大的降低了分析效率。同时，很多无法得到及时更新的分析工具，在面对层出不穷的新型攻击方式时，则显得捉襟见肘。

而现阶段很多二进制分析工具（系统仿真、用户模式仿真、二进制插桩工具和沙箱）， 都只针对单一类型的操作系统或CPU架构，且这些工具间几乎不可能共享信息或交叉引用数据。 这就是逆向工程的困难所在。

---
<h1>谁使用了麒麟框架</h1>
- 安全研究人员
     - 使用麒麟进行物联网、恶意软件、UEFI和MBR研究
     - 在麒麟框架上构建新工具，如恶意软件沙盒或模糊测试
- 大学生
     - 大学生（包括硕士和博士）在麒麟框架的基础上，通过添加新功能或构建新工具来撰写论文
- 讲师
     - 教学生如何建立操作系统
     - 解释系统调用、CPU或文件系统如何工作的最简单方法

---
<h1>什么是麒麟框架</h1>
麒麟框架不仅仅是一个仿真平台或逆向工程工具。它还将“二进制插桩”和“二进制仿真”结合一起。解决了应用程序不能在真空中运行并且高度依赖于操作系统的问题。由于大量的操作系统支持，麒麟框架为二进制分析提供了无限的可能性和潜力。借助麒麟框架，你可以：

  - 跨平台：Windows、MacOS、Linux、BSD、UEFI、DOS
  - 跨体系结构：X86、X86 64位、Arm、Arm 64位、MIPS、8086
  - 多种文件格式：PE、MachO、ELF、COM
  - 在隔离环境中模拟沙盒机器代码
  - 支持跨体系结构和平台调试功能
  - 提供高级API来设置和配置沙盒
  - 细化检测：允许不同级别的钩子（指令/基本块/内存访问/异常/系统调用/IO等）
  - 允许动态热补丁运行代码，包括加载的库


麒麟框架能够模拟：
  - Windows x86 32/64位
  - Linux x86 32/64位，ARM，AARCH64，MIPS
  - MacOS x86 32/64位
  - FreeBSD x86 32/64位
  - UEFI
  - DOS
  - MBR

麒麟框架能够在Linux/MacOS/FreeBSD/Windows(WSL2)等操作系统上运行，且不受CPU架构所限制

---

<h1>麒麟框架是如何操作的</h1>
##### 演示环境
- *Hardware : X86 64位*
- *OS : Ubuntu 18.04 64位*

##### 演示#1 如何用IDAPro和麒麟框架解简单的CTF题目
用IDAPro和麒麟框架解简单的CTF题目

[<img src="https://raw.githubusercontent.com/qilingframework/zh/master/images/demo1.jpg" width="500">](https://www.bilibili.com/video/av93142763 "演示#1 如何用IDAPro和麒麟框架解简单的CTF题目")

---
##### 演示#2 麒麟框架进行模糊测试
利用麒麟框架进行模糊测试，更多信息查询[这里](https://github.com/qilingframework/qiling/tree/dev/examples/fuzzing/README.md).

[<img src="https://raw.githubusercontent.com/qilingframework/qilingframework.github.io/master/images/qilingfzz.png" width="500">](https://raw.githubusercontent.com/qilingframework/qilingframework.github.io/master/images/qilingfzz.png "演示#2 麒麟框架进行模糊测试")

###### 代码样本
[代码样本](https://github.com/qilingframework/qiling/blob/dev/examples/fuzzing/fuzz_x8664_linux.py)

---
##### 演示#3 在Ubuntu X64位上模拟ARM路由器固件
麒麟框架动态补丁及模拟ARM路由器固件，把其/usr/bin/httpd在X86_64位 Ubuntu上运行

[<img src="https://raw.githubusercontent.com/qilingframework/zh/master/images/demo3.jpg" width="500">](https://www.bilibili.com/video/av65935353 "演示#3 在Ubuntu X64位上模拟ARM路由器固件")

###### 代码样本

```python
import os, socket, sys, threading
sys.path.append("..")
from qiling import *

def patcher(ql):
    br0_addr = ql.mem.search("br0".encode() + b'\x00')
    for addr in br0_addr:
        ql.mem.write(addr, b'lo\x00')

def nvram_listener():
    server_address = 'rootfs/var/cfm_socket'
    data = ""
    
    try:  
        os.unlink(server_address)  
    except OSError:  
        if os.path.exists(server_address):  
            raise  

    # Create UDS socket  
    sock = socket.socket(socket.AF_UNIX,socket.SOCK_STREAM)  
    sock.bind(server_address)  
    sock.listen(1)  
  
    while True:  
        connection, client_address = sock.accept()  
        try:  
            while True:  
                data += str(connection.recv(1024))
        
                if "lan.webiplansslen" in data:  
                    connection.send('192.168.170.169'.encode())  
                elif "wan_ifname" in data:
                    connection.send('eth0'.encode())
                elif "wan_ifnames" in data:
                    connection.send('eth0'.encode())
                elif "wan0_ifname" in data:
                    connection.send('eth0'.encode())
                elif "wan0_ifnames" in data:
                    connection.send('eth0'.encode())
                elif "sys.workmode" in data:
                    connection.send('bridge'.encode())
                elif "wan1.ip" in data:
                    connection.send('1.1.1.1'.encode())
                else: 
                    break  
                data = ""
        finally:  
                connection.close() 

def my_sandbox(path, rootfs):
    ql = Qiling(path, rootfs, output = "debug")
    ql.add_fs_mapper("/dev/urandom","/dev/urandom")
    ql.hook_address(patcher ,ql.loader.elf_entry)
    ql.run()


if __name__ == "__main__":
    nvram_listener_therad =  threading.Thread(target=nvram_listener, daemon=True)
    nvram_listener_therad.start()
    my_sandbox(["rootfs/bin/httpd"], "rootfs")
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
from qiling.os.uefi.const import *

def force_notify_RegisterProtocolNotify(ql, address, params):
    event_id = params['Event']
    if event_id in ql.loader.events:
        ql.loader.events[event_id]['Guid'] = params["Protocol"]
        # let's force notify
        event = ql.loader.events[event_id]
        event["Set"] = True
        ql.loader.notify_list.append((event_id, event['NotifyFunction'], event['NotifyContext']))
        ######
        return EFI_SUCCESS
    return EFI_INVALID_PARAMETER


if __name__ == "__main__":
    with open("rootfs/x8664_efi/rom2_nvar.pickel", 'rb') as f:
        env = pickle.load(f)
    ql = Qiling(["rootfs/x8664_efi/bin/TcgPlatformSetupPolicy"], "rootfs/x8664_efi", env=env)
    ql.set_api("hook_RegisterProtocolNotify", force_notify_RegisterProtocolNotify)
    ql.run()
```
