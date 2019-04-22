---
layout: post
title: "Quick Charge를 이용하여 12V 출력하기"
categories: Tech
---

Qualcomm의 Quick Charge 2.0/3.0 규격은 보조배터리에도 많이 탑재되어 휴대기기의 빠른 충전을 돕고 있다.  
<!--excerpt-->
그런데 스마트기기가 아닌 일반 장치를 연결할 경우 USB의 D-/D+ 라인에서 통신이 이루어지지 않으므로 5V만을 출력하기 때문에, 9V/12V 출력을 사용하려면 저항 4개와 ATtiny13 정도의 작은 마이크로프로세서가 필요하다.

## Parts

- ATtiny13A
- LM1117 등 3.3V LDO
- 0.1uF 칩세라믹 캐패시터
- 10k 칩저항 2개
- 2.2k 칩저항 2개

## Quick Charge Protocol

QC3.0은 QC2.0 규격에 대해 하위호환을 지원하는데, 전압 출력은 다음과 같다.

| 출력전압(V) | D- 라인 전압(V) | D+ 라인 전압(V) |
| :-------: | :---: | :---: |
| 12 | 0.6 | 0.6 |
| 9 | 0.6 | 3.3 |
| 5 | 0.6 | GND |

QC의 Handshake 과정은 다음과 같다.

1. 요청하는 측(단말)에서 1,250ms동안 D+을 0.6V로 낮춘다.
2. 충전기 측에서 이어져 있던 D-와 D+ 라인을 끊고 D-와 GND 사이에 20k의 풀다운 저항을 연결한다.
3. 충전기 측에서 이후에 일어나는 D- 라인의 전압 변화를 감지한다.

따라서 5V 이외의 전압을 출력하고 싶다면 최소 1.25초 이상 D+를 0.6V로 낮춰준 이후 D- 라인의 전압을 바꿔주면 된다.  

## Circuit

ATtiny13은 내부 오실레이터를 사용하고, GPIO 핀 4개를 각각 PinA - 10k - D-/D+ - 2.2k - PinB와 같이 2개씩 짝을 지어 사용하면 된다.  
출력전압 예는 다음과 같다.

| PinA | PinB | 출력전압(V) |
| :---: | :---: | :---: |
| 0V | 0V | 0V |
| 3.3V | 0V | 0.6V |
| 3.3V | 3.3V | 3.3V |

리셋 핀을 제외하면 인터럽트 가능한 핀이 하나 남으므로 그 핀을 사용해 전압 변경용 인터럽트 루틴을 만들어 줘도 된다.

## Code

개략적인 코드는 다음과 같다.

```c
#define F_CPU 8000000UL
#include <avr/io.h>
#include <util/delay.h>

void QCInit() {
    // PB2 - 10k - DP - 2.2k - PB0
    // PB4 - 10k - DM - 2.2k - PB3
    // 따라서 PB3, PB4는 초기에 Floating
    DDRB = (1<<DDRB0) | (1<<DDRB2) | (0<<DDRB3) | (0<<DDRB4);
    PORTB = (1<<DDRB2);
}

void QC12V() {
    // DP, DM 모두 0.6V를 필요로 하므로 모두 출력
    DDRB = (1<<DDRB0) | (1<<DDRB2) | (1<<DDRB3) | (1<<DDRB4);
    PORTB = (1<<DDRB2) | (0<<DDRB0) | (1<<DDRB4) | (0<<DDRB3);
}

int main(void) {
    QCInit();
    _delay_ms(2000); // 확실하게 하기 위해 2초 기다림
    QC12V();

    while(true) {
    }
}
```

위 코드를 가지고 ATmega8A로 테스트해본 결과 문제 없이 12V가 출력되므로 위의 부품들을 이용해 작게 만들어 LED 램프나 Li-ion 충전기의 전원으로 사용하면 좋을 것 같다.

## Added 2019-04-22

실험을 해 본 결과 마이크로컨트롤러 없이 Comparator IC 하나와 간단한 RC회로로 타이머를 이용해 Monostable Oscillator를 만들어 9V/12V 출력이 가능했다.  
어차피 D+ 라인은 0.6V로 항상 끌어내려야 하니, D- 라인만 1.25s동안 floating 상태로 두면 되므로 PNP 트랜지스터를 Comparator Output에 달아 사용하면 된다.  
추가적인 내용은 아래에 회로도를 그려 두었으니 참고하시길.

![Schematic](/assets/img/2019-04-19/schematic.png)