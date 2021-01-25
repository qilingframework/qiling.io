---
title: Introduction
sticky: 999
---

Qiling Framework is corss platform and multi arch ultra lightweight emulator. Supported OS like Linux, MacOS, Windows, FreeBSD, DOS and UEFI. It also able to emulate x86 (16, 32 and 64bit), ARM, ARM64, MIPS, EVM and WASM.  

<!-- more -->

It also support Linux Kernel Module(.ko) , Windows Driver(.sys) and MacOS Kernel(.kext) via [Demigod](https://groundx.io/demigod/).

Binary instrumentation and API are Qiling Framework main focus and priority. It is designed for reverse engineers - thus there is no need to rebuild another sand boxing tool. Using Qiling Framework saves you time. The API-rich Qiling Framework brings reverse and instrument binary to the next level quicker. 

Additionally, Qiling provides API access to register, memory, filesystem, operating system and debuger. Qiling also provides virtual machine level API such as save and restore execution state.

Qiling also made its way to various international conferences:

2020:

- [Black Hat, Europe](https://www.blackhat.com/eu-20/arsenal/schedule/index.html#qiling-framework-deep-dive-into-obfuscated-binary-analysis-21781)
- [Black Hat, USA](https://www.blackhat.com/us-20/arsenal/schedule/index.html#qiling-framework-from-dark-to-dawn-----enlightening-the-analysis-of-the-most-mysterious-iot-firmware--21062)
- [Black Hat, Asia](https://www.blackhat.com/asia-20/arsenal/schedule/index.html#qiling-lightweight-advanced-binary-analyzer-19245)
- [Hack In The Box, Lockdown 001](https://conference.hitb.org/lockdown-livestream/)
- [Hack In The Box, Lockdown 002](https://conference.hitb.org/hitb-lockdown002/virtual-labs/virtual-lab-qiling-framework-learn-how-to-build-a-fuzzer-based-on-a-1day-bug/)
- [Hack In The Box, Cyberweek](https://cyberweek.ae/2020/lab-qiling-framework/)
- [Nullcon](https://nullcon.net/website/goa-2020/speakers/kaijern-lau.php)
    
2019:

- [Defcon, USA](https://www.defcon.org/html/defcon-27/dc-27-demolabs.html#QiLing)
- [Hitcon](https://hitcon.org/2019/CMT/agenda)
- [Zeronights](https://zeronights.ru/report-en/qiling-io-advanced-binary-emulation-framework/)

<h1>Why Do We Need Qiling Framework</h1>
The insecurity of smart Internet-connected or so-called “IoT” devices has become more concerning than ever. The existence of malware exploiting vulnerabilities, often poorly secured and configured Internet-facing devices has been known for many years. Hardware vendors and the entire security industry are struggling to fight the adversaries while trying to build better and safer products. Unfortunately, IoT threats and malware analysis remain the two biggest challenges in the security industry.

Modern IoT threats and malware are moving towards various platforms and CPU architecture. Reverse engineers are struggling to cope and understand different operating systems and CPU architecture. Besides, lack of updated tools makes the situation worse. Current available tools are nowhere near to catch up with the speed of fast-growing security threat.

Common techniques used to perform analysis such as full system emulation, user-mode emulation, binary instrumentation, disassembler and sandboxing are just barely sufficient. These tools are either serving single type operating system or works on one CPU architecture. Also, these tools need to be used separately, streamlining information or cross referencing data is almost impossible. These are the reasons why reverse engineering is never an easy task.

---
<h1>Who Uses Qiling Framework</h1>
- Security Researchers
    - Using Qiling For IoT, malware, UEFI and MBR research
    - Building new tools on top of Qiling Framework such as malware sandbox or fuzzer
- University Student
    - University students (including master and PhD), writing their thesis based on adding new features or building new tools on top of Qiling Framework
- University Lecturer
    - Teaching students how to build Operating System
    - Easiest way to explain how syscall, CPU or filesystem works

---
<h1>What is Qiling Framework</h1>
Qiling Framework is not just an emulation platform or a reverse engineering tool. It combines binary instrumentation and binary emulation into one single framework, solving the problem that applications do not run in a vacuum and are highly dependent on the OS. With vast OS support, Qiling Framework opens up endless possibilities and potential for binary analysis. With Qiling Framework, it is able to:

- Cross platform: Windows, MacOS, Linux, BSD, UEFI, DOS
- Cross architecture: X86, X86_64, ARM, ARM64, MIPS, 8086
- Multiple file formats: PE, MachO, ELF, COM
- Emulate & sandbox machine code in an isolated environment
- Support cross architecture and platform debugging capabilities
- Provide high level API to setup & configure the sandbox
- Fine-grain instrumentation: allow hooks at various levels (instruction/basic-block/memory-access/exception/syscall/IO/etc)
- Allow dynamic hotpatch on-the-fly running code, including the loaded library
- True framework in Python, making it easy to build customized security analysis tools on top

Qiling Framework is able to emulate: 
- Windows X86 32/64bit
- Linux X86 32/64bit, ARM, AARCH64, MIPS
- MacOS X86 32/64bit
- FreeBSD X86 32/64bit
- UEFI
- DOS
- MBR

Qiling Framework is able to run on top of Linux/FreeBSD/MacOS/Windows (WSL2) without CPU architecture limitation

---

<h1>How Qiling Framework Works</h1>
##### Demo Setup

  - *Hardware : X86 64bit*
  - *OS : Ubuntu 18.04 64bit*

##### Demo #1 Solving simple CTF challenge with Qiling Framework and IDAPro
Mini Qiling Framework tutorial : how to work with IDAPro

[![qiling DEMO 1: Catching wannacry's killer switch](https://raw.githubusercontent.com/qilingframework/qilingframework.github.io/master/images/demo1-en.jpg)](https://www.youtube.com/watch?v=SPjVAt2FkKA "Video DEMO 1")

---
##### Demo #2 Fuzzing with Qiling Unicornalf
More information on fuzzing with Qiling can be found [here](https://github.com/qilingframework/qiling/tree/dev/examples/fuzzing/README.md).

[![qiling DEMO 2: Fuzzing with Qiling Unicornalf](https://raw.githubusercontent.com/qilingframework/qilingframework.github.io/master/images/qilingfzz-s.png)](https://raw.githubusercontent.com/qilingframework/qilingframework.github.io/master/images/qilingfzz.png "Demo #2 Fuzzing with Qiling Unicornalf")


---
##### Demo #3 Emulating ARM router firmware on Ubuntu X64 machine
Qiling Framework hot-patch and emulates ARM router's /usr/bin/httpd on a X86_64Bit Ubuntu

[![qiling DEMO 3: Fully emulating httpd from ARM router firmware with Qiling on Ubuntu X64 machine](https://raw.githubusercontent.com/qilingframework/qilingframework.github.io/master/images/demo3-en.jpg)](https://www.youtube.com/watch?v=Nxu742-SNvw "Demo #3 Emulating ARM router firmware on Ubuntu X64 machine")

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
        
                if "wan1.ip" in data:
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
##### Demo #4 Emulating UEFI
Qiling Framework emulates UEFI

[![qiling DEMO 4: Emulating UEFI](https://raw.githubusercontent.com/qilingframework/qilingframework.github.io/master/images/demo4-s.png)](https://raw.githubusercontent.com/qilingframework/qilingframework.github.io/master/images/demo4-en.png "Demo #4 Emulating UEFI")

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
