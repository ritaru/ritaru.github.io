---
layout: post
title: "Dash Crab용 Inrush Current Limiter 제작"
categories: Tech
---

# Preface

필자는 자동차에 핸드폰을 거치하기 위해 Dash Crab을 사용하고 있다.  
와디즈인가? 에서 구입한 것 같은데, 조금 하자가 있다.
<!--excerpt-->
차량의 QC 3.0 지원 충전기에 물려둔 채로 시동을 걸면 Dash Crab이 작동을 하지 않는 것이다.  
아마도 내부에 있는 Super Capacitor가 Inrush Current를 수 A ~ 수십 A정도 발생시켜서 Polyfuse가 열리는 게 아닌가 싶은데, 이 때문에 Inrush Current를 어느정도 완화해 줄 장치를 만들었다.

## Device

장치는 간단하다.  
그냥 NMOS 하나에 RC Low-Pass Filter와 Capacitor를 방전시켜줄 저항 하나만 있으면 된다.

[![schematic.png](/assets/img/2020-04-02/schematic.png)](/assets/img/2020-04-02/schematic.png)

그렇다고 막 아무 굴러다니는 FET를 쓸 수는 없는데, 적당히 RDS(on)값이 적은 것을 사용해야 FET가 뜨거워지지 않고 사용할 수 있다.

위 회로에서는 IRFZ44N(RDS(on) 17.5mOhms Max)를 사용하였는데, 이 경우 Drain을 출력 측 GND에 연결하여 서서히 Voltage Potential이 5V+와 VCOM 사이에 증가하도록 하였다.

물론, 이와 같은 사용은 사실 추천되는 방법은 아니다. 제대로 장치를 만드려면 아무래도 PMOS가 있어야 하는데, 마침 집에 널린 게 IRFZ44N이라 어쩔 수 없이 NMOS로 구성한 것.

대충 만능기판에 만들어 보았는데, 꽤 괜찮은 것 같다.  
5V+와 VCOM 사이의 Voltage Difference가 5V에 도달하기까지 약 20ms의 시간이 소요되는 것으로 볼 때 어느정도 Inrush Current를 방지해줄 것 같다.

만약 Curve가 좀 더 완만한 것을 원한다면 C1 값을 증가시키거나, R1 값을 증가시키면 된다.

생각보다 쓰루홀 소자를 써서 그런지 최종 크기가 좀 커졌다(...)

~~만들 때 좀 제대로 만들어라 좀~~