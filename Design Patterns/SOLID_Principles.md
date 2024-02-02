# SOLID 원칙

## SOLID 원칙이란?
- 객체 지향 프로그래밍 및 설계의 다섯 가지 기본 원칙.
- 시간이 지나도 유지 보수와 확장이 쉬운 시스템을 만들고자 할 때 이 원칙을 적용할 수 있다.

<br/>

## S.O.L.I.D 5가지 원칙
![images_teo_post_9e7ed0fd-2f89-41f8-a0b3-523c0c715560_image](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/a14e9c99-5e7b-4564-9810-29a90046eee6)

### 1. Single responsibility principle (단일 책임 원칙)
- 객체는 오직 하나의 책임을 가져야 한다.

### 2. Open/Closed Principle (개방-폐쇄 원칙)
- 소프트웨어 요소는 확장에는 열려 있으나 변경에는 닫혀 있어야 한다.
- 새로운 기능이 추가될 때는 기존 코드의 수정 없이 추가가 되어야 하고, 내부 매커니즘이 변경이 될 때는 외부의 코드 변화가 없어야 한다는 것을 의미한다.

### 3. Liskov substitution principle (리스코프 치환 원칙)
- 프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야 한다.
- 리스코프 치환 원칙은 상속을 받아 만든 하위 타입의 제약 조건들이 상위 타입에서 먼저 선언한 조건들과 충돌이 날 경우 유지보수가 힘들어 진다는 문제점이 있기 때문에 만들어진 것이다.
- 따라서 하위 타입의 가변성으로 인해 상위 타입에서 정의한 조건과 일치하지 않는다면 상속을 받지 말아야 한다.

### 4. Interface segregation principle (인터페이스 분리 원칙)
- 사용자가 필요하지 않은 것들에 의존하게 되지 않도록, 인터페이스를 작게 유지한다.

### 5. Dependency inversion principle (의존관계 역전 원칙)
- 프로그래머는 추상화에 의존해야지, 구체화에 의존하면 안 된다. 의존성 주입은 이 원칙을 따르는 방법 중 하나다.
- 추상화하는 방향으로 의존한다. 상위 레벨 모듈이 하위 레벨 세부 사항에 의존해서는 안 된다.

<br/>

## Reference
- [Javascript에서도 SOLID 원칙이 통할까?](https://velog.io/@teo/Javascript%EC%97%90%EC%84%9C%EB%8F%84-SOLID-%EC%9B%90%EC%B9%99%EC%9D%B4-%ED%86%B5%ED%95%A0%EA%B9%8C)
