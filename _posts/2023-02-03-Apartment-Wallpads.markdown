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

| 신호 표기 | 설명 | 현대통신 대응 신호 표기 | 기존 연결 여부 |
| :---: | :---: | :---: | :---: |
| TIP | 전화선 + | TIP | O |
| RING | 전화선 - | RING | O |
| AA1 | 경비실 Data Line 추정 | LA1 | O |
| AA2 | 경비실 Data Line 추정 | LA2 | O |
| AB1 | 경비실 Data Line 추정 | LB1 | O |
| AB2 | 경비실 Data Line 추정 | LB2 | O |
| AC1 | 경비실 Data Line 추정 | LC1 | O |
| AC2 | 경비실 Data Line 추정 | LC2 | O |
| MSTA | Master RS-485 A 추정 | LD1 추정 | O |
| MSTB | Master RS-485 B 추정 | LD2 추정 | O |
| DA | RS-485 Data A 추정 | SCA 추정 | O |
| DB | RS-485 Data B 추정 | SCB 추정 | O |
| ? | 세대 현관 영상 GND 추정 | GND | O |
| CS | 세대 현관 영상 신호 (Camera Signal) 추정 | DVS | O |
| LVSH | 공동현관(Lobby) 영상 신호 High | LVSH | O |
| LVSN | 공동현관(Lobby) 영상 신호 GND | LVS | O |
| LVD | 분배기(DISTRIBUTE) 전원 추정 | DISTRIBUTE | X |

또, 현관 도어벨 관련 신호로 추정되는 신호들은 다음과 같다.

| 신호 표기 | 설명 | 현대통신 대응 신호 표기 | 기존 연결 여부 |
| :---: | :---: | :---: | :---: |
| VSO3 | Video Signal Output 3 추정. Video 3 + |  | X |
| -GND | Video Signal GND 추정. | V-(GND) | X |
| VSO2 | Video Signal Output 2 추정. Video 2 + |  | X |
| -GND | Video Signal GND 추정. | V-(GND) | O |
| VSO1 | Video Signal Output 1 추정. 세대 현관 영상. Video 1 + | VO | O |
| -STB | RS-485 Signal B 추정 | SC2B 추정 | O |
| -STA | RS-485 Signal A 추정 | SC2A 추정 | O |
| AS2 | Audio Signal 2 추정. Audio + | LS2 | O |
| AS1 | Audio Signal 1 추정. Audio - | LS1 | O |

이외에 SUB쪽 신호는 다음과 같다.

| 신호 표기 | 설명 | 현대통신 대응 신호 표기 | 기존 연결 여부 |
| :---: | :---: | :---: | :---: |
| SUB(+) | 주방 서브 컨트롤러용 RS-485 + 추정 | SUB(+) | O |
| SUB(-) | 주방 서브 컨트롤러용 RS-485 - 추정 | SUB(-) | O |
| FIRE(+) | 화재 감지기 전원 + 추정 | FIRE(+) | O |
| FIRE(S) | 화재 감지기 신호선 추정 | FIRE(S) | O |
| BG1(+) | 방범 센서 1 전원 + 추정 | BGS(+) | O |
| BG1(S) | 방범 센서 1 신호선 추정 | BGS1 | O |
| BG2(+) | 방범 센서 2 전원 + 추정 | BGS(+) | X |
| BG2(S) | 방범 센서 2 신호선 추정 | BGS2 | X |
| GAS(+) | 가스 누설 탐지기 전원 + 추정 | GAS(+) | O |
| GAS(-) | 가스 누설 탐지기 전원 -(GND) 추정 | GAS(-) | O |
| GAS(S) | 가스 누설 탐지기 신호선 추정 | GAS-S | O |
| EMG1 | Emergency Signal 1. 비상용 신호 1 | EMG1 | X |
| EMG2 | Emergency Signal 2. 비상용 신호 2 | EMG2 | X |
| OPEN1 | 현관문 개폐 센서(Reed Switch) 신호 추정 | DO1 | O |
| OPEN2 | 현관문 개폐 센서(Reed Switch) 신호 추정 | DO2 | O |
| F.G-GND | Front Gate-GND 추정 |  | X |

추후 확인하는 대로 신호에 대한 정리는 업데이트 할 예정이다.
