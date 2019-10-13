---
layout: page
title: Installation guide
permalink: /install/
---

Qiling Framework works with different operating system and not limit to any CPU architecture.

For this installation guide, Ubuntu desktop 18.04.3 LTS 64bit is the base example. Grab a copy of official Ubuntu ISO images from [Ubuntu CD mirrors](https://launchpad.net/ubuntu/+cdmirrors). Update and the system and also install pip3, git and cmake
```
sudo apt-get update
sudo apt-get upgrade
sudo apt install python3-pip git cmake
```

Once completed, clone from github.com Qiling Framework source and run setup to install it.
```
git clone https://github.com/qilingframework/qiling
cd qiling
sudo python3 setup.py install 
```

---

#### Important note on Windows DLLs and registry

Due to distribution restriction, Qiling Framework will not bundle Microsoft Windows DLL files and registry. Please copy respective DLLs and registry from Microsoft Windows System. Normally in C:\Windows\system32 and place it in $rootfs/dlls


Refer to [DLLX86.txt](https://github.com/qilingframework/qiling/blob/master/docs/DLLX86.txt) for Windows 32bit DLLs hashes and file version

Refer to [DLLX8664.txt](https://github.com/qilingframework/qiling/blob/master/docs/DLLX8664.txt) for Windows 64bit DLLs hashes and file version

To export Windows Registry from Windows
```
ntuser hive : C:\Users\Default\NTUSER.DAT 
reg save hklm\system SYSTEM
reg save hklm\security SECURITY
reg save hklm\software SOFTWARE
reg save hklm\SAM SAM
```
