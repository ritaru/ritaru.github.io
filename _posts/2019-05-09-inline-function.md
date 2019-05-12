---
layout: post
title: "인라인 함수와 컴파일 타임"
categories: Tech
---

최근에 수업에서 사용할 라이브러리를 만들기 위해 조금 공부를 할 일이 있었다.  
<!--excerpt-->

```c
// myLib.h
#ifndef F_CPU
#warning Please define F_CPU
#define F_CPU 10000000UL
#endif

// myLib.c
#include "myLib.h"
uint16_t frequency() {
    return F_CPU
}
```

```c
// main.c
#define F_CPU 8000000UL
#include "myLib.h"

int main(void) {
    printf("%ld\n", F_CPU);
    printf("%ld\n", frequency());
    return 0;
}
```

이때의 나는 무식했기 때문에, 당연히 출력 결과는 8000000UL로 동일할 것이라 오판했다.
하지만 실제 결과는 다음과 같다.

```text
8000000
10000000
```

이유는 Preprocessor의 동작 과정을 보면 알 수 있다.

1. main.c를 컴파일 하기 전에 myLib.c를 컴파일함
2. myLib.h에서 F_CPU는 #ifndef ~ #endif clause에 의해 F_CPU = 10000000으로 대치됨.

```c
uint16_t frequency() {
    return 10000000;
}
```

3. main.c의 컴파일 타임에는 Preprocessor가 F_CPU를 8000000으로 대치하므로 컴파일 직전의 코드는 다음과 같음.

```c
#include "myLib.h"
int main(void) {
     printf("%ld\n", 8000000);
    printf("%ld\n", frequency());
}
```

4. 생성된 목적 파일 myLib.o, main.o를 gcc 링커가 dependency check를 통해 main.o에서 myLib.o의 frequency() 함수를 필요로 하므로 myLib.o를 main에 Static Link함.
5. 링크된 실행 파일이 생성됨.

따라서 출력 결과는 위와 같이 서로 다른 결과가 나온다.  
그렇다면 이 문제를 해결하기 위해서는 어떻게 해야 할까?  

답은 크게 두 가지가 있다.

1. gcc 링커에 -include 옵션을 주어 소스들을 컴파일 할 때마다 필요한 정의들이 담긴 main.h를 포함시킨다.
2. gcc 링커에 -D 옵션을 주어 Global Label 필드를 정의한다.

해외에서도 어떤 것이 나은 지에 대한 의견이 분분한데, 아무래도 Global Label을 매 번 정해주는 것보다는 헤더 파일을 따로 하나 만들어 두고 필요한 정의들을 나열해 두는 편이 나는 더 깔끔한 것 같아 1번을 택했다.

그런데 이런 귀찮은 일들을 하지 않아도 되는 방법이 있긴 하다.

바로 Inline Function을 사용하는 것인데, 보통 컴파일러는 정의된 함수를 호출할 때 성능 상 어느 것이 이로운지 판단하여 inline function으로 컴파일하거나 아니면 branch를 통해 함수를 호출할 지 결정한다.  
그런데 이런 Inline function을 강제하기 위해서는 보통 함수명 앞에 static inline을 붙여 헤더 파일에 함수를 구현한다.
이럴 경우 따로 헤더 파일을 만들어 컴파일 타임마다 추가시켜야 하는 귀찮은 일들을 할 필요가 없지만, 성능 상에 손해를 보는 경우가 많다(프로그램 사이즈가 커진다).  
따라서 정말 필요한 경우가 아니라면 그냥 컴파일러가 알아서 자기 일을 하도록 두는 것이 좋다.

오늘의 배움
1. Static Link 과정
2. 컴파일 과정
3. 인라인 함수의 사용