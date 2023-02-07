---
layout: post
title: "현대디지텍 HDS-6900를 현대통신 제품으로 교체 시도 #1"
categories: Tech
---

## Preface

아파트에 입주할 당시에 설치된 월패드 LCD 드라이버가 드디어 맛이 갔다.  
문제는 현대디지텍이 폐업했기 때문에 호환되는 제품을 찾을 수 없어 설치업자에게 의존하여야 한다는 것.  

<!--exerpt-->

설치업자에게 연락을 해 보니 가격도 가격이지만 현대통신 제품과 현대디지텍 제품은 호환되지 않아 따로 변환 모듈을 설치해야 하는데, 이 변환 모듈을 만드는 사람이 개인이라고 한다.  

당연히 판매자를 물어봤지만 답은 해 주지 않았다.

그럼 뭐 별 수 있겠는가, 현대통신 제품과 현대디지텍 제품의 차이를 내가 직접 분석해서 변환 모듈을 만들어 쓰던가 해야지.

일단 사전 조사를 위해 집의 월패드를 뜯었다.

그리고 세대 내로 인입되는 신호를 보면 다음과 같다.

| 신호 표기 | 설명 | 현대통신 대응 신호 표기 | 기존 연결 여부 | 비고 |
| :---: | :---: | :---: | :---: | :---: |
| TIP | 전화선 + | TIP | O | 무극성 |
| RING | 전화선 - | RING | O | 무극성 |
| AA1 | 경비실 통화 A회선 | LA1 | O | 유극성 |
| AA2 | 경비실 통화 A회선 | LA2 | O | 유극성 | 
| AB1 | 경비실 통화 B회선 | LB1 | O | 유극성 | 
| AB2 | 경비실 통화 B회선 | LB2 | O | 유극성 | 
| AC1 | 경비실 통화 C회선 | LC1 | O | 유극성 | 
| AC2 | 경비실 통화 C회선 | LC2 | O | 유극성 | 
|  | 경비실 통화 D회선 | LD1 | X | 별도 설명 참조[^1] | 
|  | 경비실 통화 D회선 | LD2 | X | | 
| MSTA | Master RS-485 A 추정 | SCA 추정 | O | TBD |
| MSTB | Master RS-485 B 추정 | SCB 추정 | O | TBD |
| DA | Door Open Signal 추정 | ? | O | TBD |
| DB | Door Open Signal 추정 | ? | O | TBD |
| ? | 세대 현관 영상 GND 추정 | GND | O | 도어/로비 그라운드 분리 |
| CS | 세대 현관 영상 신호 (Camera Signal) 추정 | DVS | O | 75ohm 1Vp-p |
| LVSH | 공동현관(Lobby) 영상 신호 High | LVS | O | 75ohm 1Vp-p |
| LVSN | 공동현관(Lobby) 영상 신호 GND | GND | O | 도어/로비 그라운드 분리 |
| LVD | 분배기(DISTRIBUTE) 전원 추정 | DISTRIBUTE 또는 DTB+ | X | 별도 설명 참조[^2] |

주방 컨트롤러 등 보조 컨트롤러 관련 신호는 다음과 같다. 

| 신호 표기 | 설명 | 현대통신 대응 신호 표기 | 기존 연결 여부 | 비고 |
| :---: | :---: | :---: | :---: | :---: |
| VSO3 | Video Signal Output 3 |  | X | 결선시 75ohm 종단저항 처리 필요<br />Sub CH1 영상과 동일 신호. |
| -GND | Video Signal GND | D-GND(공통) | X | 공통 GND |
| VSO2 | Video Signal Output 2 | SVS2 | X | Sub CH2 영상 회선.<br />75ohm 종단저항 처리 필요<br />Sub CH1 영상과 동일 신호. |
| -GND | Video Signal GND | D-GND(공통) | O | 공통 GND |
| VSO1 | Video Signal Output 1 | SVS1 | O | Sub CH1 영상 회선.<br />75ohm 종단저항 처리 필요 |
| -STB | RS-485 Signal B 추정 | SC2B 추정 | O | Sub-Phone 통신 회선 |
| -STA | RS-485 Signal A 추정 | SC2A 추정 | O | Sub-Phone 통신 회선 |
| AS2 | Audio Signal 2 | LS2 | O | Sub-Phone 통화 회선 |
| AS1 | Audio Signal 1 | LS1 | O | Sub-Phone 통화 회선 |

이외에 SUB쪽 신호는 다음과 같다.

| 신호 표기 | 설명 | 현대통신 대응 신호 표기 | 기존 연결 여부 | 비고 |
| :---: | :---: | :---: | :---: | :---: |
| SUB(+) | 보조전원 +12V 추정 | SUB(+) | O |
| SUB(-) | 보조전원 GND 추정 | SUB(-) | O |
| FIRE(+) | 화재 감지기 전원 +24V | FIRE(+) | O | DC 24V, 무극성 |
| FIRE(S) | 화재 감지기 GND | FIRE(-) | O | DC 24V, 무극성 |
| BG1(+) | 동체감지기 센서 전원 + | LOAD12V | O |
| BG1(S) | 동체감지기 센서 신호. | ZONE2 | O | Normally Closed |
| BG2(+) | 방범 센서 2 전원 + 추정 | LOAD12V | X |
| BG2(S) | 방범 센서 2 신호선 추정 | ZONE3/4 | X | Normally Closed |
| GAS(+) | 가스 누설 탐지기 전원 + | GAS(+) | O | DC 12V / 150mA |
| GAS(-) | 가스 누설 탐지기 GND | GAS(-) | O |
| GAS(S) | 가스 누설 탐지기 신호선 | GAS(S) | O |
| EMG1 | Emergency Signal 1. 비상용 신호 1 | EMG1 | X | Normally Open |
| EMG2 | Emergency Signal 2. 비상용 신호 2 | EMG2 | X | Normally Open |
| OPEN1 | 현관문 개폐 센서(Reed Switch) 신호 추정 | ZONE1 | O | 규격 확인 필요 |
| OPEN2 | 현관문 개폐 센서(Reed Switch) 신호 추정 | D-GND | O | 규격 확인 필요 |
| F.G-GND | Front Gate-GND 추정 |  | X |

추후 확인하는 대로 신호에 대한 정리는 업데이트 할 예정이다.

<style>
.footnotes {
    font-size: 0.8rem;
}
</style>

---
<div class="footnotes" markdown="1">
[^1]: 현대디지텍 주장치(HMS-100)은 기본적으로 LA ~ LC 3채널밖에 없다. LD는 무시한다.  
[^2]: 영상 절체기 DISTRIBUTE+(또는 DTB+)를 연결하는 터미널이 없는 경우 제어선을 본체에 연결되는 케이블 중 하나에 연결한다.  
HNT-3079 기준 CN107 1번 핀에 T형 커넥터로 연결한다.
</div>