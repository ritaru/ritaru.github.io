---
layout: post
title: "Brymen BU-86X DIY"
categories: Tech
---

# Preface

최근에 Brymen BM869s를 선물로 받았다.  
기존에 사용하던 Uni-T UT39C를 드디어 처분할 수 있어서 기뻤다.  
UT39C의 경우 전류계가 맛가서 제대로 측정이 되지 않는 상태로 쓰고 있었는데, 근 10년 만에 멀티미터를 교체하는 것이다.  

<!--excerpt-->

한 가지 달성하고 싶은 게 있었는데, 작업 책상에서 컴퓨터를 켜 두고 자료를 보면서 각종 계측기도 전부 sigrok으로 연동하여 SmuView로 보는 것이었다.  

이 목표를 달성하기 위해서는 일단 새로 받은 멀티미터부터 sigrok에 연동시켜야 하는데 문제가 있다.  
Brymen BM869s의 경우 USB 연결이 가능하나, 동일 제조사의 BU-86X라는 어댑터를 사용해야만 가능하다.  

다행히 EEVBlog의 사람들 중 한 명이 프로토콜을 분석해 USB Bridge를 설계하여 배포[^1] 중이다.  
STM32G030F 기반으로, IR Transistor와 IR LED를 사용해 BM869s와 통신하여 UART로 데이터를 보내면 SmuView에서 볼 수 있는 방식이다.  

이 프로젝트에서 사용하는 부품의 경우 흔히 이용하는 엘레파츠, 디바이스마트 등의 사이트에서 구하기 쉽다.  

다만, 일부 수입이 어려운 품목이 있어 적당히 대체 가능한 것으로 BOM을 적어본다.

## Bill of Materials

| 품목명 | 필요수량 | 패키지 | 비고 |
| :---: | :---: | :---: | :---: |
| STM32F030F4P6 | 1 | TSSOP-20 | |
| HT42B534-2 | 1 | SOIC-8 | |
| 24C08 | 1 | SOT23-5 | 적당히 싼 것으로. |
| TSAL6100 | 1 | T-1 3/4(5mm) | |
| ORH-G35A | 1 | T-1 3/4(5mm) | LL-503PTC2 대체 |
| Generic LED | 1 | 0805(2012 Metric) | |
| 10uF / 10V MLCC | 1 | 0805(2012 Metric) | |
| 1uF / 25V MLCC | 1 | 0805(2012 Metric) | |
| 100nF / 50V MLCC | 2 | 0805(2012 Metric) | |
| 2.2k 1/8W | 2 | 0805(2012 Metric) | |
| 1k 1/8W | 1 | 0805(2012 Metric) | |
| 750R 1/8W | 2 | 0805(2012 Metric) | |
| SMD Tact Switch | 1 | 5.2 x 5.2mm, 4p, 1.5mm height | |
| USB 케이블 | 1 | | 적당히 |

## Making

TBD.  
부품이 오면 작성할 예정이다.  

PCB의 경우 Github Repository에 원작자가 제작한 Eagle CAD PCB Artwork 및 Gerber File이 있다.  
Firmware 및 소스 코드도 공개하고 있으니 아래 링크를 확인 바란다.  

<style>
.footnotes {
    font-size: 0.8rem;
}
</style>

---
<div class="footnotes" markdown="1">
[^1]: 원본 블로그 글: [http://embedblog.eu/?p=830](http://embedblog.eu/?p=830)<br />Github Repository: [https://github.com/MartinD-CZ/BrymenConnector21](https://github.com/MartinD-CZ/BrymenConnector21)
</div>