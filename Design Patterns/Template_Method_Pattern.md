# Template Method Pattern

## 템플릿 메서드 패턴이란?
- **알고리즘의 기본적인 구조를 상위 클래스에 정의한 뒤 부분적으로 필요한 구체적인 구현을 하위 클래스에서 처리하도록 디자인 된 패턴**을 템플릿 메서드 패턴이라고 한다.

<br/>

## 템플릿 메서드 예시
```javascript
class Benefit {
  constructor() {
    this.startDate = SETTING.eventStartDate;
    this.endDate = SETTING.eventEndDate;
    this.reservedDate = Order.getInstance().getReservedDate();
  }

  isValid() {
    if (
      this.startDate <= this.reservedDate && 
      this.reservedDate <= this.endDate
    ) {
      return true;
    }
    return false;
  }

  getBenefit() {
    return { name: '', amount: 0 };
  }

  applyBenefit(benefits) {
    const benefit = this.getBenefit();
    benefits[`${benefit.name}`] = benefit.amount;
    return benefits;
  }
}
```
- 공통의 로직을 포함하는 추상 클래스 `Benefit`을 정의한다.
- `getBenefit`처럼 기본 행동만 정의되어 있으며 실제 필요한 내용은 하위 클래스에서 구현하도록 하는 메서드를 **후크(Hook) 메서드**라 부른다.

<br/>

```javascript
class SpecialDayBenefit extends Benefit {
  constructor() {
    super();
  }

  isValid() {
    if (
      this.startDate <= this.reservedDate &&
      this.reservedDate <= this.endDate &&
      SETTING.specialEventDayPeriod.includes(this.reservedDate.getDate())
    ) {
      return true;
    }
    return false;
  }

  getBenefit() {
    return {
      name: BENEFIT_NAME.specialDayBenefit,
      amount: SETTING.specialEventDiscountAmount,
    };
  }
}
```
- `Benefit`을 상속받는 하위 클래스들을 정의한다. 예를 들어 특정 기간 내에 특정 날짜에만 적용되는 할인 내용을 담은 `SpecialDayBenefit`는 다음과 같이 작성할 수 있다.
-  `isValid`와 `getBenefit` 메서드가 자신의 비즈니스 로직에 맞게 새로 구현된 것을 볼 수 있다. 상위 클래스(`Benefit`)에서 정한 메서드의 이름은 그대로 사용하지만, 구현 내용은 하위 클래스에서 다르게 정의하는 것이다.
-  이처럼 상위 클래스로부터 상속된 메서드를 재정의하여 사용하는 것을 **메서드 오버라이딩(Method Overriding)** 이라고 한다.

<br/>

```javascript
// this.#benefitItems에 모든 각 혜택 클래스들의 배열이 저장되어 있다고 가정한다.
this.#benefitItems.forEach((benefitItem) => {
  if (benefitItem.isValid()) {
    benefits = benefitItem.applyBenefit(benefits);
  }
});
```
- 개별 혜택 클래스들을 순회하는 `BenefitHandler` 클래스의 코드를 살펴보면, 각각의 혜택 클래스들에 대하여 `isValid` 메서드로 적용 가능 여부를 판별한 뒤, `applyBenefit` 메서드로 `benefits` 객체에 혜택 적용 내역을 추가시킨다. 이때 `benefits` 객체에 추가되는 내용은 각 클래스 내부에 위치한 `getBenefit` 메서드가 정한다.
- 공통 로직을 해치지만 않는다면, 언제든 원하는 유형의 새로운 혜택 클래스를 간편하게 만들고 관리할 수 있다.

<br/>

## 장점
- 코드의 재사용성과 유연성이 증가하고 알고리즘 구현 구조를 명확하게 드러냄으로써 유지보수 또한 쉬워진다.

<br/>

## 단점
- 개별 하위 클래스 구현의 유연성을 얻는 대신, 상위 클래스 알고리즘의 구조 변경에는 상대적으로 취약해지기 때문에 남용할 경우 클래스 계층 구조가 복잡해질 수 있다.

<br/>

## Reference
- [우아한테크코스 6기 프리코스 과정에서 배운 세 가지 디자인 패턴](https://seongjin.me/woowacourse-three-design-patterns-in-javascript/?utm_source=oneoneone)
