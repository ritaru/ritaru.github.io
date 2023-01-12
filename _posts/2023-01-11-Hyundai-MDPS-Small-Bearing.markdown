---
layout: post
title: "현대자동차 아반떼 CN7 MDPS 스몰 베어링 교체"
categories: Tech
---

# Preface

현대자동차의 C-MDPS는 소나타 DN8을 비롯하여 이전부터 스몰 베어링 마모 이슈가 있어 핸들 조향시 소음이 보고되었고, 이는 미국 NHTSA (도로교통안전국)에도 C-MDPS Worm Shaft Bearing Noise와 관련하여 [TSB(Technical Service Bulletin)](https://static.nhtsa.gov/odi/tsbs/2021/MC-10203272-0001.pdf)이 등록되어 있다.

<!--excerpt-->

현대자동차의 2021년 이전 모델들은 MDPS에 NMB Thailand제 626D[^1]가 장착되어 빈번하게 소음 문제가 보고되었고, 이에 대한 해결책으로 현대차는 동일 제조사의 608D 베어링을 채택하여 그 크기를 키웠으나 여전히 소음 문제가 보고되고 있다.

## WHY

나는 아반떼 CN7을 2020년 7월에 인도받고 이후로 19,000km째 타고 있는데, 보통 90,000~100,000km에 발생해야 할 C-MDPS Worm Shaft Small Bearing 소음 문제가 벌써 발생하여 짜증이 이만저만이 아니다.

글을 적으면서도 화가 나는 부분은 이 어떠한 내용을 나는 현대자동차로부터 고지받은 적도 없고, [WPC(Web Parts Catalogue)](https://wpc.mobis.co.kr/)[^2]를 통한 부품 조회에서도 교체 부품을 찾을 수 없고, [GSW(Global Service Way)](https://gsw.hyundai.com/hmc/login.tiles)[^3]에 정말 간략하게 설명이 되어 있다.

그래서 정말 몇 없는 정보를 찾아 헤매다 아반떼 CN7에 해당하는 [C-MDPS Worm Shaft Bearing Noise TSB](https://static.nhtsa.gov/odi/tsbs/2022/MC-10215599-0001.pdf)를 구글 검색을 통해 찾을 수 있었고, 이에 대해 적고자 한다.

## Repair Procedure

필요 항목은 다음과 같다.

| 품목명 | 수량 | 링크 | 비고 |
| :---: | :---: | :---: | :---: |
| 복스 핸들 3/8" | 1 |  | 망치 대용으로 사용해야 할 수도 있으니 튼튼한 것으로. |
| 복스 소켓 | 1 | | 10mm 이상.<br />608ZZ의 경우 전용 특수공구[^4]가 없을 경우 사용한다. |
| 복스 연장대 | 1 | | 너무 긴 것이 아니면 된다.<br />소켓의 경우 짧으므로 타격 시 어려움이 있어 사용한다. |
| 육각 렌치 | 1 | | 추후 사이즈 추가 예정. |
| 실리콘 그리스 | 1 | [Super Lube Silicon Grease](https://smartstore.naver.com/yc0944/products/7223498671) | Silicon Grease 사용 필수.<br />보통 신에츠社 제품을 많이 사용.<br />나의 경우 SKF社의 Silicon Grease를 사용했다. |
| MDPS 스몰 베어링 풀러 | 1 | [네이버 스토어](https://smartstore.naver.com/s09com/products/6696618258) | 베어링 풀러의 경우 626/608 모두 사용 가능. |
| 자석 자바라 | 1 | [네이버 스토어](https://smartstore.naver.com/s09com/products/2001512169) | 고정 스프링, 핀을 빼기 위해 필요.<br />필수는 아니나 있으면 좋음 |
| SKF 608ZZ/C3 | 1 | [네이버 스토어](https://smartstore.naver.com/wibearings/products/6159809135) | C3 이상 사용할 것, Axial Load가 있을 수 있음.<br />일본산 베어링 역시 마찬가지로 짧은 수명이 보고됨. |
| 베어링 키트 | 1 | [파츠로](https://partsro.com/) | 626ZZ의 경우 [56359-L1AAAFFF](http://partsro.com/product/detail.html?product_no=836998).<br />608ZZ는 [56358-AAAAAFFF](https://partsro.com/front/php/product.php?product_no=856798).<br />플라스틱 커버 적용 차량의 경우 커버가 일회용이므로 필수.<br />Sliding Damper의 경우도 재장착하는 것을 권장하지 않는다. |

[![RSJF9298.jpg](/assets/img/2023-01-11/RSJF9298.jpg)](/assets/img/2023-01-11/RSJF9298.jpg)
*Radial Internal Clearance(위 제품의 경우 C3)을 꼭 확인하고 구입하여야 한다.*

SKF의 경우 다국적 기업으로 여러 곳에서 생산된 제품을 받을 수 있다.  
나의 경우 이탈리아 생산 제품을 받았다.  
일본제 베어링에 비해 작동 신뢰성이 우수한 것으로 알려져 있긴 하지만, 어차피 소모품이기에 큰 기대는 하지 않는다.

[![RSJF9301.jpg](/assets/img/2023-01-11/RSJF9301.jpg)](/assets/img/2023-01-11/RSJF9301.jpg)
*56358-AAAAAFFF. Sliding Damper가 파란 색인 것이 특징이다.* 

그러면 본격적으로 작업을 시작하자.

1. 웨더스트립 탈거
    - 밑의 항목들을 진행하기 위해서는 웨더스트립을 제거해야 편하다.
2. 프런트 도어 스커프 트림 탈거
    - 발 닿는 부분의 플라스틱 트림인데, 정비지침에는 스크류 드라이버나 리무버를 사용하여 탈거할 것으로 되어 있지만 손으로 슥슥 잡아 당기면 빠진다.
3. 후드 랫치 릴리스 핸들 탈거
    - 본네트 후드 여는 핸들. 적당히 잘 잡아당기면 빠진다.
4. 카울 사이드 트림 탈거
    - 약간 난이도가 있는 편인데, 이 녀석도 적당히 잘 안 부러지게끔 잡아당기면 빠진다.
5. 크래쉬 패드 로어 패널 탈거
    - 좌측 나사 3개, 우측 하단 나사 1개를 빼고 좌측부터 분리하면 빠진다.
    
        [![RSJF9323.jpg](/assets/img/2023-01-11/RSJF9323.jpg)](/assets/img/2023-01-11/RSJF9323.jpg)
        *좌측 나사 부분* 

        [![RSJF9321.jpg](/assets/img/2023-01-11/RSJF9321.jpg)](/assets/img/2023-01-11/RSJF9321.jpg)
        *우측 나사 부분* 

    - 분리 후 OBD 단자를 탈거한다.
    
        [![RSJF9322.jpg](/assets/img/2023-01-11/RSJF9322.jpg)](/assets/img/2023-01-11/RSJF9322.jpg)
        *OBD 단자* 

6. C-MDPS Worm Shaft Small Bearing 고정용 핀 커버, 스프링, 핀 탈거
    - 육각 렌치를 사용하여 커버를 풀고, 내부의 스프링과 고정핀을 탈거한다.
    - Y렌치의 경우 공간이 좁고 주변 전선과 간섭이 있으므로 육각 렌치 등 좁은 공간에서 사용 가능한 도구로 커버를 풀어야 한다.
    - 스프링과 고정핀은 핀셋 등을 사용해도 되지만 작업 시 자석 자바라를 사용하는 것이 편하다.  
    
        [![RSJF9299.jpg](/assets/img/2023-01-11/RSJF9299.jpg)](/assets/img/2023-01-11/RSJF9299.jpg)
        *스프링, 고정 핀이 장착되어 있는 부분.* 

        [![RSJF9304.jpg](/assets/img/2023-01-11/RSJF9304.jpg)](/assets/img/2023-01-11/RSJF9304.jpg)
        *커버를 탈거한 모습.* 

        [![RSJF9306.jpg](/assets/img/2023-01-11/RSJF9306.jpg)](/assets/img/2023-01-11/RSJF9306.jpg)
        *좌측부터 순서대로 스프링, 고정 핀, 커버. 고정 핀은 저 방향대로 삽입하여 그 뒤 스프링을 삽입한다.* 

    
7. 하단 베어링 커버 제거
    - 플라스틱 커버 장착 차량의 경우 6개의 탭을 전부 부숴서 빼야 한다.  
    재사용이 불가능한 구조로 되어 있으니 새 것을 이후에 장착한다.

        [![RSJF9320.jpg](/assets/img/2023-01-11/RSJF9320.jpg)](/assets/img/2023-01-11/RSJF9320.jpg)
        *베어링 커버* 

        [![RSJF9312.jpg](/assets/img/2023-01-11/RSJF9312.jpg)](/assets/img/2023-01-11/RSJF9312.jpg)
        *Sliding Damper. 핀셋 또는 롱노즈 플라이어를 사용해 제거한다. 재사용하지 않는다.* 

8. 베어링 탈거
    - 전용 특수공구[^5] 또는 MDPS 스몰 베어링 풀러 등을 사용하여 베어링을 탈거한다.  
    이 때 수공구만을 사용하고 전동 라쳇핸들 등을 사용하지 않는다.

        [![RSJF9313.jpg](/assets/img/2023-01-11/RSJF9313.jpg)](/assets/img/2023-01-11/RSJF9313.jpg)
        *3/8인치 라쳇 핸들을 끼워 시계 방향으로 돌리면 빠진다.*     

9. 그리스 세척 및 재도포
    - 과도한 그리스를 베어링 키트에 동봉된 스틱 및 IPA를 이용하여 제거 및 청소한 뒤 실리콘 그리스를 재도포한다.
    - 이 때 과도포하지 않는다.
    
        [![RSJF9316.jpg](/assets/img/2023-01-11/RSJF9316.jpg)](/assets/img/2023-01-11/RSJF9316.jpg)
        *이 정도만 윤활해도 충분하다.*     
10. 베어링 압입
    - 타격하여 압입하는 경우는 주의한다.
    - 압입 시 중앙부 샤프트가 베어링 샤프트보다 약간 돌출되어야 한다. 돌출되지 않은 경우 Sliding Damper 장착 후 고정 핀이 삽입 불가능하다. 해당 내용은 [TSB](https://static.nhtsa.gov/odi/tsbs/2022/MC-10215599-0001.pdf)를 참조한다.
11. Sliding Damper 장착
    - 고정 핀 방향에 맞추어 Sliding Damper를 장착한다.
12. 고정 핀, 스프링, 커버 장착
    - 고정 핀, 스프링, 커버를 IPA로 세척한 뒤 순서대로 고정핀, 스프링을 장착한 후 그리스를 소량 도포, 그리고 커버를 장착한다.
13. 플라스틱 트림 및 릴리스 핸들, 크래쉬 패드 로어 패널 장착
    - 위 순서의 역순으로 각 부품을 조립한다.

### Side note
위와 같은 과정을 거치고 시동을 건 후, 핸들을 조향하여 소음이 있는지 확인한다.  
또, 핸들 조향과 관련하여 MDPS 영점이 틀어지지는 않았는지 정지 시 확인한다.  
주행 시에도 마찬가지로 영점과 소음을 확인한다. 이상이 있는 경우 1급 정비소를 방문하여 점검을 받아야 한다.

### After
나의 경우 10번 단계에서 복스 연장대를 챙겨가지 않아 베어링 풀러를 이용해 압입했다. ~~**이러면 안 된다.**~~
아무튼, 이후에 핸들 조향 시 소음이 사라진 것을 확인하였고 영점이 틀어진 것 같진 않았다.  
고속 주행 시에도 핸들이 안정적으로 조향되는 것을 보니 당분간은 문제가 없을 것 같다.

<style>
.footnotes {
    font-size: 0.8rem;
}
</style>

---
<div class="footnotes" markdown="1">
[^1]: D는 커버가 고무이고, ZZ타입은 커버가 금속 재질이다.
[^2]: 부품 상세 검색 사이트
[^3]: 현대자동차 수리 및 기술 정보 사이트, 가입 필요
[^4]: 09563-IB200
[^5]: 0K563-L2100FFF
</div>
