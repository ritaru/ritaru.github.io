---
layout: post
title: "현대자동차 아반떼 CN7 MDPS 스몰 베어링 교체"
categories: Tech
---

# Preface

현대자동차의 C-MDPS는 소나타 DN8을 비롯하여 이전부터 스몰 베어링 마모 이슈가 있어 핸들 조향시 소음이 보고되었고, 이는 미국 NHTSA (도로교통안전국)에도 C-MDPS Worm Shaft Bearing Noise와 관련하여 [TSB(Technical Service Bulletin)](https://static.nhtsa.gov/odi/tsbs/2021/MC-10203272-0001.pdf)이 등록되어 있다.

<!--excerpt-->

현대자동차의 2021년 이전 모델들은 MDPS에 NMB Thailand제 626D<sup>[1](#footnote_1)</sup>가 장착되어 빈번하게 소음 문제가 보고되었고, 이에 대한 해결책으로 현대차는 동일 제조사의 608D 베어링을 채택하여 그 크기를 키웠으나 여전히 소음 문제가 보고되고 있다.

## WHY

나는 아반떼 CN7을 2020년 7월에 인도받고 이후로 19,000km째 타고 있는데, 보통 90,000~100,000km에 발생해야 할 C-MDPS Worm Shaft Small Bearing 소음 문제가 벌써 발생하여 짜증이 이만저만이 아니다.

글을 적으면서도 화가 나는 부분은 이 어떠한 내용을 나는 현대자동차로부터 고지받은 적도 없고, WPC<sup>[2](#footnote_2)</sup>를 통한 부품 조회에서도 교체 부품을 찾을 수 없고, GSW<sup>[3](#footnote_3)</sup>에 정말 간략하게 설명이 되어 있다.

그래서 정말 몇 없는 정보를 찾아 헤매다 아반떼 CN7에 해당하는 [C-MDPS Worm Shaft Bearing Noise TSB](https://static.nhtsa.gov/odi/tsbs/2022/MC-10215599-0001.pdf)를 구글 검색을 통해 찾을 수 있었고, 이에 대해 적고자 한다.

## Repair Procedure

필요 항목은 다음과 같다.

| 품목명 | 수량 | 링크 | 비고 |
| :---: | :---: | :---: | :---: |
| 복스 핸들 3/8" | 1 |  | 시중품 어떤 것이든 사용 가능.</br>망치 대용으로 사용해야 할 수도 있으니 튼튼한 것으로. |
| 실리콘 그리스 | 1 | [Super Lube Silicon Grease](https://smartstore.naver.com/yc0944/products/7223498671) | Silicon Grease 사용 필수, 보통 신에츠社 제품을 많이 사용 |
| MDPS 스몰 베어링 풀러 | 1 | [네이버 스토어](https://smartstore.naver.com/s09com/products/6696618258) | 베어링 풀러의 경우 626/608 모두 사용 가능하나, 장착 공구는 사용 불가능.</br>장착 시 복스알 사용 필요 |
| 자석 자바라 | 1 | [네이버 스토어](https://smartstore.naver.com/s09com/products/2001512169) | 고정 스프링, 핀을 빼기 위해 필요.</br>필수는 아니나 있으면 좋음 |
| SKF 608ZZ/C3 | 1 | [네이버 스토어](https://smartstore.naver.com/wibearings/products/6159809135) | C3 이상 사용할 것, Axial Load가 있을 수 있음.</br>NTN, NSK 등 일본산 베어링 역시 NMB제 베어링과 마찬가지로 짧은 수명이 보고됨. |
| 베어링 키트 | 1 | [파츠로](https://partsro.com/front/php/product.php?product_no=856798&) | 626ZZ의 경우 [56359-L1AAAFFF](http://partsro.com/product/detail.html?product_no=836998) 사용. 현대 부품 번호 56358-AAAAAFFF.</br>플라스틱 커버 적용 차량의 경우 커버가 일회용이므로 반드시 필요하다.</br>Sliding Damper의 경우도 재장착하는 것을 권장하지 않는다. |

[![RSJF9298.jpg](/assets/img/2023-01-11/RSJF9298.jpg)](/assets/img/2023-01-11/RSJF9298.jpg)

SKF의 경우 다국적 기업으로 여러 곳에서 생산된 제품을 받을 수 있다. </br>
나의 경우 이탈리아 생산 제품을 받았다.



<a name="footnote_1">[1]</a> D는 커버가 고무이고, ZZ타입은 커버가 금속 재질이다. </br>
<a name="footnote_2">[2]</a> [WPC(Web Parts Catalogue)](https://wpc.mobis.co.kr/), 부품 상세 검색 사이트 </br>
<a name="footnote_3">[3]</a> [GSW(Global Service Way)](https://gsw.hyundai.com/hmc/login.tiles), 현대자동차 수리 및 기술 정보 사이트, 가입 필요 </br>
