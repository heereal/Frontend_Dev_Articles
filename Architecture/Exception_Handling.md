# Exception Handling 예외 처리
> [좋은 예외(Exception) 처리](https://jojoldu.tistory.com/734)
- 복구 가능한 오류와 불가능한 오류를 구분한다.
   - 복구 가능한 오류: 시스템 외적인 요소로 발생하는 치명적이지 않은 오류
   - 복구 불가능한 오류: 별도의 조치 없이 시스템이 자동으로 복구할 수 있는 방법이 없는 경우
- null, -1, 빈 문자열 등의 특수값을 예외로 사용하지 않는다.
- 단순 문자열이 아닌 Error 객체를 throw 한다. 
```javascript
throw new IllegalArgumentException(`사용자 ${userId}의 입력(${inputData})가 잘못되었다.`);
```
- 추적 가능한 예외를 throw한다.
- 예외의 이름에는 그 예외의 원인과 내용 등의 명확한 의미를 담는다.
- Layer에 맞는 예외를 throw한다.
- 외부 SDK, 외부 API를 통해 발생하는 예외들은 하나로 묶어서 처리한다.
- 가능한 가장 늦은 위치에서 예외를 처리한다.
