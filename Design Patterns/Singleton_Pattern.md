# Singleton Pattern

## 싱글턴 패턴이란?
- 싱글턴 패턴은 애플리케이션 안에서 **특정 클래스의 인스턴스가 오직 하나만 생성되도록 제한**하는 디자인 패턴이다.
- 특정 객체가 애플리케이션의 여러 영역에서 동일한 상태를 유지해야 할 때, 혹은 그 객체에 대해 전역적인 접근 지점을 제공해 주어야 할 때 활용할 수 있다.

<br/>

## 싱글턴 패턴 예시
```javascript
class Menu {
  #items;

  constructor() {
    // 이미 생성된 인스턴스가 존재하는지 체크한다.
    if (Menu.instance) {
      return Menu.instance;
    }

    // 만약 없다면, 새 인스턴스를 생성 후 저장한다.
    this.#items = {};
    Menu.instance = this;
  }

  addMenuItem(name, price, category) {
    this.#items[name] = { price, category };
  }

  // 전역에서 인스턴스 호출 가능한 static 메서드를 정의한다.
  static getInstance() {
    if (!Menu.instance) {
      Menu.instance = new Menu();
    }
    return Menu.instance;
  }

  // 필요시 인스턴스 초기화를 위한 static 메서드도 정의한다.
  static resetInstance() {
    if (Menu.instance) {
      Menu.instance = null;
    }
  }

  ...
}
```
- `Menu` 클래스에 담긴 정보는 애플리케이션 전역에 걸쳐 동일성이 유지되어야 한다.
- 따라서 `Menu` 클래스에 대한 인스턴스가 하나만 존재할 수 있도록 하고, 코드 전역에서 해당 인스턴스를 불러올 수 있는 내용을 클래스 안에 추가했다.
- 이렇게 구현하면 `Menu` 클래스를 이용한 인스턴스 생성을 시도할 때마다 항상 동일한 인스턴스가 반환된다.
- 또한 애플리케이션 안에서는 `getInstance` 메서드를 통해 언제든지 `Menu` 클래스로 생성된 단일 인스턴스에 접근할 수 있다.
- 애플리케이션 전체에서 공통적으로 사용되어야 하는 메뉴 정보를 단일 인스턴스로 관리함으로써 데이터의 일관성을 지킬 수 있다.

<br/>

## 싱글턴 패턴 장점
1. 객체의 불필요한 중복 생성을 방지하여 시스템 자원의 낭비를 줄일 수 있다.
2. 애플리케이션 전체에서 공통으로 사용되는 리소스에 대해 일관된 접근 방식을 제공할 수 있다.
3. 애플리케이션 전역에서 객체에 접근할 수 있으므로, 별도의 파라미터 전달이나 의존성 주입과 같은 과정이 필요 없다.

<br/>

## 싱글턴 패턴 단점
1. 싱글턴 객체가 사용된 코드에서는 단위 테스트(Unit Test) 수행이 어려워진다. 단일 인스턴스가 애플리케이션 코드의 여러 영역에 걸쳐 공유되어야 하는데, 이는 작은 기능 단위로 나뉘어 서로 독립적으로 수행되어야 하는 테스트를 구현하는 과정에 큰 어려움을 가져온다.
2. 멀티스레드 환경처럼 다수의 클라이언트가 동시에 접근할 때 발생하는 객체의 상태 변화에 유의해야 한다. 이런 환경에서 싱글턴 객체의 동기화가 보장되지 않는다면, 이에 의존하는 코드에 다양한 오류를 발생시킬 수 있다.
3. 싱글턴 패턴을 사용한 객체 구현은 객체의 리소스를 캡슐화하고, 외부로부터 은닉한다는 객체 지향적 설계 원칙에 어긋날 수 있다.

<br/>

## Reference
- [우아한테크코스 6기 프리코스 과정에서 배운 세 가지 디자인 패턴](https://seongjin.me/woowacourse-three-design-patterns-in-javascript/?utm_source=oneoneone)
