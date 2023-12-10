# Chain of Responsibility Pattern

## 책임 연쇄 패턴이란?
<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/b3f2bd52-1722-445b-b35f-0aa639370894" width="500px" >

- 책임 연쇄 패턴은 **요청을 처리할 객체들의 연결 구조를 만들어 책임을 전달하는 방식으로 설계된 패턴**이다.
- 책임 연쇄 패턴을 사용함으로써 클라이언트의 요청을 처리할 객체들 간의 결합도를 낮출 수 있다.
- 책임 연쇄 패턴은 일반적으로 **클라이언트(Client)** 와 **핸들러(Handler)**, 그리고 실제 요청 처리를 담당하는 **구체 핸들러(ConcreteHandler)** 를 구성요소로 가진다.
- 핸들러가 클라이언트로부터 메시지를 받아 구체 핸들러들의 연결체로 작업 처리의 책임을 넘기는 구조를 가지고 있다.

<br/>

## 책임 연쇄 패턴 예시 
```javascript
class BenefitHandler {
  #benefitItems;

  constructor() {
    this.#benefitItems = this.#createBenefits();
  }

  #createBenefits() {
	// 각각의 혜택 내용을 담은 클래스들의 배열을 생성한다.
    const benefitItems = [
      new ChristmasDDayBenefit(),
      new WeekdayBenefit(),
      new WeekendBenefit(),
      new SpecialDayBenefit(),
      new FreeMenuItemBenefit(),
    ];
    return benefitItems;
  }

  getBenefits() {
    let benefits = {};

    // 혜택 적용에 필요한 최소 구매 금액 조건을 만족하는지 검증한다.
    if (!this.#isMetConditionToApplyBenefit()) {
      return benefits;
    }

    // 개별 혜택 클래스를 순회하면서 적용 가능한 혜택 내용을 benefits에 추가한다.
    this.#benefitItems.forEach((benefitItem) => {
      if (benefitItem.isValid()) {
        benefits = benefitItem.applyBenefit(benefits);
      }
    });

    // 이렇게 하여 종합된 benefits 객체를 반환시킨다.
    return benefits;
  }

  #isMetConditionToApplyBenefit() {
    const totalOrderedAmount = Order.getInstance().getTotalOrderedAmount();
    if (totalOrderedAmount < SETTING.minOrderAmountForEvent) {
      return false;
    }
    return true;
  }
}
```
- `createBenefits` 메서드를 보면 개별 혜택 내용이 포함된 서브 클래스들이 배열 안에 포함된 것을 알 수 있다. 
- 이 각각의 클래스에는 해당 혜택을 적용 가능한 조건인지 체크하는 `isValid` 메서드와 인자로 전달 받은 `benefits` 객체에 자신의 혜택 내용을 추가시키는 `applyBenefit` 메서드가 포함되었다. 
- `benefitHandler`는 클라이언트가 `getBenefits` 메서드를 호출했을 때 이 클래스들을 순회한 뒤 결과값을 반환하는 역할만 수행한다.

<br/>

## 장점
1. 애플리케이션 구조에 유연성과 확장성을 높일 수 있다. 클라이언트 요청 처리에 필요한 객체를 추가하거나 수정하는 작업, 혹은 요청 처리 순서를 변경하는 작업이 모두 간편해진다.
2. 각 객체에 대한 단일 책임 원칙을 반영하기 용이하다. 역시 코드의 유지보수 및 확장에 도움이 된다.

<br/>

## 단점
1. 책임 연쇄 패턴을 사용한 코드에서는 요청 처리가 가능한 객체를 찾을 때까지 순회가 이루어지므로 컴퓨팅 자원의 낭비가 발생할 수 있다. 앞서 살펴본 `BenefitHandler` 코드를 예시로 살펴본다면, `benefitItems` 체인 안에서 어떠한 혜택도 받을 수 없는 경우 결과값은 빈 값({})이 된다. 클라이언트의 메시지를 처리하기 위해 체인 안의 모든 객체들이 돌아가며 연산을 수행했으나 얻은 것이 없는 것이다. 
2. 이 패턴에서 활용할 모든 체인은 반드시 **일방향 비순환 그래프(Directed Acyclic Graph; DAG)** 구조여야 한다. 필요에 따라 여러 종류의 체인을 구성하거나 체인 안에 분기 처리를 해야 할 상황도 생길텐데, 이 경우 체이닝 구성에 주의하지 않으면 순환구조가 발생할 수 있다.

<br/>

## Reference
- [우아한테크코스 6기 프리코스 과정에서 배운 세 가지 디자인 패턴](https://seongjin.me/woowacourse-three-design-patterns-in-javascript/?utm_source=oneoneone)
