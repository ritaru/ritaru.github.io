---
layout: post
title: "EOTech 오픈 도트사이트 레플리카의 수리"
categories: Airsoft
---

## Preface

최근에 EOTech社의 오픈 도트사이트 레플리카 제품을 수리할 일이 있었다.  
수리 과정을 기록해 두어야 할 것 같아서 이 글을 적는다.
<!--excerpt-->

### Build Quality 측면에서

내부 배선 상태가 매우 좋지 않은 것도 있지만 우선 전반적인 빌드 퀄리티 자체가 매우 떨어진다.  

사이트에 사용한 유리의 접합부는 Silicone Gasket Maker와 같은 재질로 아주 얇게 칠해져 있고 만들 때 대충 칠해서인지 유리 표면까지 묻어있었다.  
빛이 샐 수 있는 부분도 여러 곳 있었고, 기판을 실리콘으로 보강 처리했다고 하는데 실제로 받은 것은 핫멜트를 위에 적당히 쏘아 놓은 것 뿐, 다른 것은 없었다.  
홀리워리어나 에볼루션 기어 등 고가의 레플리카를 제외하면 배선을 완전히 갈고, LED를 교체해야 제대로 보일려나 싶다.   

다만 조절나사 등은 E형 스냅링으로 풀리지 않도록 잘 설계되어 있었고, 금속부 마감은 매우 깔끔했다.

### 작업 내용

필요한 준비물은 다음과 같다.

| 품목 | 수량 | 규격 | 비고 |
| :---: | :---: | :---: | :---: |
| 롱노즈 플라이어 | 1 | 150mm면 충분하다. | 시중품 |
| #00 십자 드라이버 | 1 | 조금 큰 녀석으로. | 시중품 |
| Torx(별) 드라이버 | 1 | 드라이버 비트 세트가 있다면 좋다. | 시중품 |
| 육각 렌치 | 1 | 3mm | 시중품 |
| 열풍기 | 1 | 100도 이하로 조절 가능한 열풍기가 있다면 좋다.<br />없을 경우 헤어드라이어로 대체 가능. | 시중품 |
| 실리콘 가스켓 접착제 | 1 | 분해 후 청소 및 재조립을 생각하고 있다면 해당 접착제를 사용한다. | [신개암](http://n-gaeam.co.kr/product/detail.html?product_no=1813&cate_no=481&display_group=1) |
| 고밀도용 접착제(흑색) | 1 | 분해 후 재조립을 하지 않을 것이라면 해당 접착제를 사용한다. | [신개암](http://n-gaeam.co.kr/product/detail.html?product_no=1816&cate_no=681&display_group=1) |
| 나사 고정제 | 1 | Loctite 222 또는 243을 사용해도 무방하다. | [신개암](http://n-gaeam.co.kr/product/detail.html?product_no=1364&cate_no=680&display_group=1) |
| 먼지 제거제 | 1 | 에어컴프레서가 있는 경우 대체 가능 | 시중품 |
| IPA | 1 | 99.9% 이상, 광학용 유리 및 PCB 세정용 | 시중품 |
| 극세사 천 | 1 | 먼지가 없는 카메라 렌즈 등에 사용하는 깨끗한 제품을 사용할 것.<br />추천은 Toraysee 제품. | 시중품 |
| IDC 케이블(컬러) | 1 | 연접된 AWG26 이상 케이블을 사용하면 된다. | [ic114](https://www.ic114.com/WebSite/site/sc/00V0.aspx?id_p=P0031792) |


이외에도 작업을 시작하려면 기본적인 공구(드라이버, 바이스, 플라이어 등)을 구비해 두는 것이 좋다.  

실제 작업 순서를 정리해 보자면,

1. 하단 Torx 스크류 제거
2. 하부 레일마운트 육각 볼트 제거 (3mm, 2개)
3. 십자 스크류 제거 (4개)
4. 측면 조절나사 고정용 E형 스냅링 제거 후 측면 조절나사 제거
5. 내부 부품 탈거(유리 및 고정부)
6. 열풍기로 매우 약하게 가열하여 배터리 삽입부 제거
7. 배선 제거 후 재작업
8. 역순으로 조립

대충 이 정도 순서가 되겠다.

<style>
.footnotes {
    font-size: 0.8rem;
}
</style>

---
<div class="footnotes" markdown="1">
</div>