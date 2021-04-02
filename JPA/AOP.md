# AOP

> AOP (Aspect-oriendted Prgramming)은 OOP를 보완하는 수단으로,
>
> 흩어진 Aspect를 모듈화 할 수 있는 프로그래밍 기법이다.



## AOP 주요 개념

- **Aspect**

  - **AOP의 기본 모듈**

  - 부가기능을 정의한 코드인 어드바이스(Advice)와 어드바이스를 어디에 적용하지를 결정하는

    포인트컷(PointCut)을 합친 개념이다.

- **Targer**

  - **Aspect**를 적용하는 곳

- **Advice**

  - 실질적인 부가기능을 담고 있는 모듈

- **Join Point**

  - **Advice**가 적용될 수 있는 위치를 말한다.
  - 생성자 호출, 메서드 진입, 필드에서 값을 꺼내 올 때, 등 다양한 시점에서 가능

- **PointCut**

  - **Join Point**의 상세한 스펙을 정의한 것.
  - Advice를 적용할 타켓의 메서드를 선별하는 정규표현식

  

