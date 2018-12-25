---
layout: post
title: "ChibiStudio 개발 환경 설정"
categories: "Tech"
---

OpenOCD와 ChibiStudio를 설치했다면 다음과 같은 환경 설정이 필요하다.  
STM32F103 기준, External Tools로 OpenOCD를 추가해야 하는데 다음과 같은 Argument를 추가해 주어야 한다.

```text
-f C:\OpenOCD\scripts\interface\stlink-v2.cfg -f C:\OpenOCD\scripts\target\stm32f1x.cfg
```

OpenOCD 경로는 적당히 알아서 수정하길 바란다.  
Debug Configuration도 이에 맞추어 변경을 해 주어야 하는데, 가장 먼저 C/C++ Application 경로를 .\build\ch.elf로 변경해준다.  
그 다음, Startup 메뉴에서 Initialization Commands에 다음과 같은 코드를 적어준다.

```text
set remotetimeout 20
monitor reset init
monitor sleep 50
```

Runtime Options에서 Set breakpoint at: main을 설정해주면 편하다.  
\* ChibiStudio로 ChibiOS 관련 Demo를 Import해올 경우 꼭 Makefile을 수정하자.  
ChibiOS Root Directory Location(\$CHIBIOS)가 변하기 때문에 빌드가 되지 않는다.

제대로 OpenOCD를 구성했을 경우 다음과 같은 콘솔 메시지가 표시된다.

```text
GNU MCU Eclipse 64-bits Open On-Chip Debugger 0.10.0+dev-00487-gaf359c18 (2018-05-12-19:30)
Licensed under GNU GPL v2
For bug reports, read
    http://openocd.org/doc/doxygen/bugs.html
WARNING: interface/stlink-v2.cfg is deprecated, please switch to interface/stlink.cfg
Info : auto-selecting first available session transport "hla_swd". To override use 'transport select <transport>'.
Info : The selected transport took over low-level target control. The results might differ compared to plain JTAG/SWD
adapter speed: 1000 kHz
adapter_nsrst_delay: 100
none separate
Info : Listening on port 6666 for tcl connections
Info : Listening on port 4444 for telnet connections
Info : Unable to match requested speed 1000 kHz, using 950 kHz
Info : Unable to match requested speed 1000 kHz, using 950 kHz
Info : clock speed 950 kHz
Info : STLINK v2 JTAG v29 API v2 SWIM v7 VID 0x0483 PID 0x3748
Info : using stlink api v2
Info : Target voltage: 3.250693
Info : stm32f1x.cpu: hardware has 6 breakpoints, 4 watchpoints
Info : Listening on port 3333 for gdb connections
```

RT-STM32F103-MAPLEMINI demo를 이용하여 Blue pill 또는 Black pill 보드의 USB-Serial 기능을 사용하려면 Makefile 중 다음 부분을 0으로 수정한다.

```Makefile
USE_MAPLEMINI_BOOTLOADER ?= 1
```

그렇지 않은 경우 빌드 후 디버깅 및 플래싱이 불가능하다.
