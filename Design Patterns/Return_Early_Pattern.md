# Return Early Pattern

## Return Early Pattern이란?
- `Return early`는 함수 또는 메소드를 작성하는 방법이다.
- 예상되는 결과는 함수의 끝에서 리턴되고, 나머지 코드는 조건을 충족하지 못했을 때 return 혹은 예외를 throw 하는 방식으로 실행문을 종료시킨다.

<br/>

## Return Early 예시 및 장점
```java
public String returnStuff(SomeObject argument1, SomeObject argument2){
      if (!argument1.isValid()) {
            throw new Exception();
      }

      if (!argument2.isValid()) {
            throw new Exception();
      }

      SomeObject otherVal1 = doSomeStuff(argument1, argument2);

      if (!otherVal1.isValid()) {
            throw new Exception();
      }

      SomeObject otherVal2 = doAnotherStuff(otherVal1);

      if (!otherVal2.isValid()) {
            throw new Exception();
      }

      return "Stuff";
}
```
- 인덴테이션이 오직 한 뎁스만 들어가있다. 이렇게 되면 선형적으로(위에서 아래로) 읽을 수 있다.
- 예상 결과를 함수 끝에서 빠르게 찾을 수 있다. 
- 예외 케이스를 먼저 처리하는 fail-first 마인드셋은 TDD와 유사하다. 이는 코드를 테스트하기 훨씬 쉽게 해준다.
- 함수는 에러가 발생하는 즉시 종료되기에, 의도하지 않게 코드가 실행될 가능성을 방지한다.

<br/>

## Reference
- [[디자인 패턴]Early return pattern이란?](https://woonys.tistory.com/entry/Design-PatternJavaEarly-return-pattern%EC%9D%B4%EB%9E%80)
- [Return Early Pattern](https://medium.com/swlh/return-early-pattern-3d18a41bba8)
