---
title: Introduction
sticky: 999
---

Cross platform and multi arch ultra lightweight emulator. Supported OS: Linux, MacOS, Windows, FreeBSD, DOS and UEFI. Support Arch: x86(16/32/64), ARM(64) MIPS, EVM and WASM.

<!-- more -->

It also support Linux Kernel Module(.ko) , Windows Driver(.sys) and MacOS Kernel(.kext) via [Demigod](https://groundx.io/demigod/).

Binary instrumentation and API are Qiling Framework main focus and priority. It is designed for reverse engineers - thus there is no need to rebuild another sand boxing tool. Using Qiling Framework saves you time. The API-rich Qiling Framework brings reverse and instrument binary to the next level quicker. 

Additionally, Qiling provides API access to register, memory, filesystem, operating system and debuger. Qiling also provides virtual machine level API such as save and restore execution state.

Qiling also made its way to various international conferences:

2021:
- [Black Hat, USA](https://www.blackhat.com/us-21/arsenal/schedule/index.html#bringing-the-x-complete-re-experience-to-smart-contract-24119)
- [Hack In The Box, Amsterdam](https://conference.hitb.org/hitbsecconf2021ams/sessions/when-qiling-framework-meets-symbolic-execution/)
- [Black Hat, Asia](https://www.blackhat.com/asia-21/arsenal/schedule/index.html#qiling-smart-analysis-for-smart-contract-22643)

2020:

- [Black Hat, Europe](https://www.blackhat.com/eu-20/arsenal/schedule/index.html#qiling-framework-deep-dive-into-obfuscated-binary-analysis-21781)
- [Black Hat, USA](https://www.blackhat.com/us-20/arsenal/schedule/index.html#qiling-framework-from-dark-to-dawn-----enlightening-the-analysis-of-the-most-mysterious-iot-firmware--21062)
- [Black Hat, USA (Demigod)](https://www.blackhat.com/us-20/briefings/schedule/#demigod-the-art-of-emulating-kernel-rootkits-20009)
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
### Who Uses Qiling Framework
#### Security Researchers
- Using Qiling For IoT, malware, UEFI and MBR research
- Building new tools on top of Qiling Framework such as malware sandbox or fuzzer
#### University Student
- University students (including master and PhD), writing their thesis based on adding new features or building new tools on top of Qiling Framework
#### University Lecturer
- Teaching students how to build Operating System
- Easiest way to explain how syscall, CPU or filesystem works

---
### What is Qiling Framework
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

### How Qiling Framework Works
The below Youtube video shows how the above example works.

#### Emulating ARM router firmware on Ubuntu X64 machine

- Qiling Framework hot-patch and emulates ARM router's /usr/bin/httpd on a X86_64Bit Ubuntu

[![qiling Tutorial: Emulating and Fuzz ARM router firmware](https://github.com/qilingframework/theme.qiling.io/blob/master/source/img/fuzzer.jpg?raw=true)](https://www.youtube.com/watch?v=e3_T3KLh2NU " Demo #3 Emulating and Fuzz ARM router firmware")

#### Qiling's IDAPro Plugin: Instrument and Decrypt Mirai's Secret

- This video demonstrate how Qiling's IDAPro plugin able to make IDApro run with Qiling instrumentation engine

[![](http://img.youtube.com/vi/ZWMWTq2WTXk/0.jpg)](http://www.youtube.com/watch?v=ZWMWTq2WTXk "Qiling's IDAPro Plugin: Instrument and Decrypt Mirai's Secret")

#### GDBserver with IDAPro demo

- Solving a simple CTF challenge with Qiling Framework and IDAPro

[![Solving a simple CTF challenge with Qiling Framework and IDAPro](https://i.ytimg.com/vi/SPjVAt2FkKA/0.jpg)](https://www.youtube.com/watch?v=SPjVAt2FkKA "Video DEMO 2")


#### Emulating MBR

- Qiling Framework emulates MBR

[![qiling DEMO: Emulating MBR](https://github.com/qilingframework/theme.qiling.io/blob/master/source/img/mbr.png?raw=true)](https://github.com/qilingframework/theme.qiling.io/blob/master/source/img/mbr.png?raw=true "Demo #4 Emulating UEFI")
