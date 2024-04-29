---
layout: post
title: "세나 50S용 배터리 구입기"
categories: Tech
date: 2024-04-27 16:00:00 +0900
---

## Preface

아직 세나 50S를 구입하진 않았지만 배터리가 빨리 상태가 나빠진다는 이야기가 있어 선제적으로 먼저 배터리를 주문했다.

<!--excerpt-->

세나 50S에 장착된 배터리는 XK952439로, KC 인증을 받은 배터리이다. (인증번호 YU10504-16002I)
그러나 9.5 (Thickness) \* 24 (Width) \* 39mm(Length) 규격의 1000mAh 배터리는 흔하지 않으므로, Shenzhen Data Power Technology LTD. (DTP)의 102540 (10 \* 25 \* 40mm) 1000mAh Li-Po 배터리를 구입했다.

이것 역시 국내에서는 유통되고 있지 않지만, DTP 社의 배터리는 다른 리튬 폴리머 배터리들로 KC 인증을 받은 사례가 있어 선정했다. (인증번호 XU100743-22009H)

알리익스프레스를 통해 구입할 경우 KC 인증도 문제지만, 성능검사를 제대로 하지 않는 경우가 많아 믿을 수 없기 때문에 Sample로 직접 공장으로부터 구매했다.

구매 시 동일 규격의 1100mAh 제품도 있었지만 Energy Density가 높아지면 그만큼 화재 등의 위험이 커지므로 그냥 기존 배터리와 동일한 용량으로 구입하였다.

## Specification

DTP 102540 1000mAh의 Cell Characteristic이다.

|                 Item                 |  Characteristics   |            비고            |
| :----------------------------------: | :----------------: | :------------------------: |
|            Rated Capacity            |      1000mAh       |                            |
|           Minimum Capacity           |      1000mAh       |                            |
|           Nominal Voltage            |        3.7V        |                            |
|         Charge Limit Voltage         |        4.2V        |                            |
|      Discharge Cut-off Voltage       |        2.4V        | Cell 자체 Cut-off 권장전압 |
|           Standard Charge            |    0.2C (200mA)    |                            |
|          Standard Discharge          |    0.2C (200mA)    |                            |
|  Maximum Continuous Charge Current   |    0.5C (500mA)    |                            |
| Maximum Continuous Discharge Current |    0.5C (500mA)    |                            |
|     Operating Temperature Range      |      0 ~ 45℃       |                            |
|            Cell Impedance            | Less than 100mohms |                            |

다음은 BMS의 Characteristic이다. BMS는 DW01을 사용하는 간단한 회로이다.

|               Item                |   Characteristic    |
| :-------------------------------: | :-----------------: |
|  Over Charge Protection Voltage   |    4.28V ±0.05V     |
| Over Discharge Protection Voltage |     3.0V ±0.1V      |
|      Over Current Protection      | Min: 2.0A Max: 5.0A |
|         Short Protection          |  Within 0.5ms Max   |

조립된 배터리의 규격은 다음과 같다.
세나 50S 배터리가 현재 없어 전선 길이는 50mm정도로 지정했다.

[![image.png](/assets/img/2024-04-27/image.png)](/assets/img/2024-04-27/image.png)

[![dtp-battery.jpg](/assets/img/2024-04-27/dtp-battery.jpg)](/assets/img/2024-04-27/dtp-battery.jpg)

실제 배터리 충방전 테스트를 진행해본 결과, 3.84V에서 3.08V까지 300mA CC Discharge시 750mAh정도가 나왔다. 충전이 덜 되어있었음을 감안한다면 1000mAh Spec에 부합할 듯 하다.

추후에 세나 배터리가 맛이 가면 이것으로 교체를 해 볼 예정이다.

## Additional Notes

세나 50S의 경우 충전 시간이 약 2.5시간, 또한 20분 충전 시 블루투스 인터콤을 2시간 사용이 가능한 급속 충전이 가능하다.

기존 배터리가 1000mAh이므로 1C = 1A이고, 블루투스 인터콤의 경우 만충시 12시간 사용이 가능하므로 약간의 계산을 해 보면 다음과 같다.

$$ \textrm{Charge Level (\%)} = {2 \over 12} * 100 \approx 16.6667\textrm{\%} $$

사용되는 공식은 다음과 같다.

$$ \textrm{W} = \textrm{P (Power)} = \textrm{V} * \textrm{I} $$

$$ x \textrm{(C)} = { {\textrm{Charge/Discharge Current(A)} \over 1.0\textrm{Ah}} }\ (x \geq 0) $$

따라서 2시간 사용을 위해서 20분 동안 16.6667%의 Capacity Charge가 이루어져야 하므로 C-Rate를 계산해 보면 다음과 같다.

$$ \textrm{Rapid Charge Rate} = { {3.7\textrm{Wh} * {2 \over 12}} \over 3.7\textrm{V} * {1 \over 3}\textrm{h} } = 1.0\textrm{A} * {6 \over 12} = 0.5\textrm{C} $$

이후에는 정상적으로 CC-CV 충전이 진행되므로, 나머지 83.3333%에 대하여 충전을 40분동안 진행한다면 다음과 같은 Charge Rate를 가진다.

$$ \textrm{Charge Rate (C)} = { {3.7\textrm{Wh} * {10 \over 12}} \over 3.7\textrm{V} * {2 \over 3}\textrm{h} } = 1.0\textrm{A} * {5 \over 4} = 1.25\textrm{C} $$

위의 Specification에서 적은 것처럼, Max Continuous Charge Rate은 0.5C로 지정되어 있다.  
Discharge Rate의 경우 특별히 걱정하지 않아도 되지만 (가장 많이 전력을 소모하는 메시 인터콤의 경우 11시간, 계산 시 소모량 약 91mAh) Charge Rate의 경우 Max Continuous Charge Rate가 상당히 적게 책정되어 있으므로 Max값에서 0.75C를 초과하여 충전해도 되는가에 대해서는 조금 생각해 볼 여지가 있다.

보통 리튬 폴리머의 경우 1.0C 기준으로 충/방전을 하도록 되어 있고, 최대로 충전하는 경우에도 2C를 초과하지 말 것을 권장하고 있다. 그러나 이 배터리는 0.5C를 기준으로 충/방전 Cycle이 잡혀 있고, 이에 따라 0.5C를 초과하여 충전할 경우 제 용량이 유지되지 않을 가능성이 크다.

또한 Battery Cycle Life 역시 줄어들어 약 300회 이하로 떨어질 것으로 보이는데, 0.5C 충방전을 기준으로 300 cycle 이후에 잔존 Capacity가 80%로 줄었기 때문이다.

이를 위해서 새로운 Spec을 정해 보았다.

|             Item             |      Characteristic      |
| :--------------------------: | :----------------------: |
|             Size             | 10 \* 25 \* 40mm or smaller  |
|        Min. Capacity         | 1000mAh (\@1C Discharge) |
| Max Charge Rate (Continuous) |           1.5C           |
|   Standard Discharge Rate    |           0.5C           |
|     Min. Battery Cycles      |        500 cycles        |

이 정도면 위의 Scenario를 충분히 만족할 것으로 보이며, 사실 정품 배터리도 0.5C 규격으로 나오지 않았을까 의심이 든다 (배터리 수명이 빨리 줄어듦).

그래서 일단 중국 제조사들을 상대로 제품을 수소문해보고 있다. 결과가 있다면 다른 포스트에 작성하겠다.
