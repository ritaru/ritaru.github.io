---
layout: post
title: "liquidctl 사용법"
categories: Tech
---

# Preface

최근에 새로 컴퓨터를 구입하면서 좀 많은 일들이 있었다.  
첫 번째로 Windows와 Linux의 듀얼 부팅을 위해서 NVMe 드라이브를 2개 설치했는데, 도저히 BIOS 메뉴를 들어갈 수 없었다.  
<!--excerpt-->  
원인을 찾고 보니 케이스에 PCIe 라이저 카드를 장착하면서 그래픽카드가 정상적으로 초기화되었어야 하는데, 보조 전원에 전원 케이블을 꽂아둔 채로 PCIe 슬롯에 그래픽카드를 장착해서 문제가 생겼던 것.  
  
두 번째로는 NZXT CAM 소프트웨어를 리눅스 환경에서 사용할 수 없다는 것이었는데, 이를 해결해주는 멋진 CLI 도구가 있었다.  
([liquidctl Github](https://github.com/jonasmalacofilho/liquidctl))
  
그런데 자꾸 Permission Error가 생기거나, 아니면 아예 liquidctl을 설치할 수 없는 문제가 있었다.  
  
이 글에서는 그 문제들을 해결하는 방법에 대해 적고자 한다. (사실상 메모용이다.)

## liquidctl 설치가 안 되는 경우

이 경우는 Prerequisite 라이브러리나 패키지가 설치되지 않은 경우인데, pip를 통해 설치하면서 로그를 주의깊게 보자. 대부분 libusb 라이브러리가 설치되지 않은 경우이다.  

Ubuntu 계열의 OS를 사용한다면 

```bash
sudo apt install libusb-1.0
```

을 통해 설치해 주자.

## liquidctl이 장치에 접근하지 못하는 경우

여기가 메인인데, 필자는 NZXT H510i(NZXT Smart Device V2)와 EVGA CLC 280(Asetek 690LC)를 사용하고 있다.  
  
윈도우야 관리자 권한을 UAC를 통해 주면 그만이지만, 리눅스의 경우 Permission을 Insecure하게 설정해 두기 싫어 udev를 통해 사용자에게 부팅 시 장치에 대한 읽기/쓰기 권한을 줄 수 있도록 설정하기로 했다.  
  
필자는 Kubuntu 18.04를 사용하고 있으며, Linux Kernel 버전은 5.5.0이다.

```bash
rita@RiTA-Kubuntu  ~/  lsusb
Bus 006 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 005 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 004: ID 1e71:2006 NZXT 
Bus 003 Device 003: ID 2433:b200  
Bus 003 Device 002: ID 05e3:0608 Genesys Logic, Inc. Hub
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 003: ID 048d:8297 Integrated Technology Express, Inc. 
Bus 001 Device 006: ID 046d:c084 Logitech, Inc. 
Bus 001 Device 005: ID 0853:0147 Topre Corporation 
Bus 001 Device 004: ID 0a12:0001 Cambridge Silicon Radio, Ltd Bluetooth Dongle (HCI mode)
Bus 001 Device 002: ID 05e3:0608 Genesys Logic, Inc. Hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

lsusb를 입력하면 현재 연결된 USB 장치들을 표시해 주는데, 여기서 눈여겨 볼 것은 NZXT와 이름이 없는 장치이다.  
  
ID의 첫 네 자리는 Vendor ID로, 어느 회사에서 제조한 제품인지 알 수 있게 해 주는 Hex 값이다.  
뒤에 콜론으로 따라오는 네 자리는 Product ID로, 어떤 제품인지 구분할 수 있게 해 주는 값.  

이제 NZXT Smart Device V2, 그리고 CLC 280의 Vendor ID, Product ID를 알았으니 udev를 설정해 보자.  
  
```ini
SUBSYSTEMS=="usb", ATTRS{idVendor}=="1e71", ATTRS{idProduct}=="2006", GROUP="plugdev", MODE="0664"
```
대부분 udev rules는 /etc/udev/rules.d/ 아래에 위치해 있다.
여기에 99-nzxt.rules라는 이름으로 필자는 NZXT를 위해 하나, 비슷한 형태로 CLC 280을 위해 하나 저장해 두었다.  
  
dd-이름.rules에서 dd는 udev가 파일을 읽는 우선순위로 99가 가장 마지막이다.  
다른 프로그램이나 데몬과 충돌하지 않도록 필자는 99-이름.rules의 형식으로 저장해 두었다.  
  
위에 있는 파일이 하는 일은, udev가 이 파일을 읽고, SUBSYSTEM, ATTR{idVendor}, ATTR{idProduct}와 일치하는 장치의 접근 권한을 그룹 이름 plugdev에게 주는 것이다.  
  
자세한 내용은 [Debian Wiki](https://wiki.debian.org/udev)를 참조하자.  
  
그룹 이름이 plugdev인 이유는 Debian 계열의 OS에서 SystemGroup 이름으로 지정해 두었기 때문이다.  
  
터미널에서 groups 명령어를 실행해 보고 자신의 계정이 plugdev에 없다면  
```
sudo usermod -aG plugdev 계정_이름
```
를 실행해주자.

이 과정을 모두 마쳤다면 재부팅을 해준 뒤, 다음과 같은 코드를 실행해 본다.

```bash
rita@RiTA-Kubuntu  ~  ls -al /dev | grep hidraw 
crw-rw-r--   1 root plugdev 236,     0  3월  9 16:33 hidraw0
```

재부팅을 했을 때 다음과 같이 Permission 설정이 되어 있다면 성공한 것이다.  
  
이제 liquidctl을 실행해 보면 다음과 같은 출력을 볼 수 있다.

```bash
rita@RiTA-Kubuntu  ~  liquidctl status
NZXT Smart Device V2 (experimental)
├── Fan 2 duty      40  %
├── Fan 2 speed    731  rpm
├── Fan 3 duty      40  %
├── Fan 3 speed    998  rpm
└── Noise level     50  dB

Asetek 690LC (assuming EVGA CLC)
├── Liquid temperature        33.8  °C
├── Fan speed                    0  rpm
├── Pump speed                1980  rpm
└── Firmware version      2.10.0.0
```

혹시 이외의 다른 문제가 발생한다면 liquidctl을 --debug 옵션을 주어 실행해 보자.