## every()가 빈 배열에 true를 반환하는 이유
> [JavaScript WTF: Why does every() return true for empty arrays?](https://humanwhocodes.com/blog/2023/09/javascript-wtf-why-does-every-return-true-for-empty-array/)   
> [(번역) 이상한 자바스크립트: 왜 every()는 빈 배열에 true를 반환할까?](https://velog.io/@sehyunny/why-does-every-return-true-for-empty-array)

<br/>

## every()란?
- Array 인스턴스의 `every()` 메서드는 **배열의 모든 요소가 제공된 함수로 구현된 테스트를 통과하는지 테스트**합니다. 이 메서드는 boolean 값을 반환합니다.
> [MDN Web Docs](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/every)

<br/>

## every()가 빈 배열에 true를 반환하는 이유
```javascript
function isNumber(value) {
    return typeof value === "number";
}

[1].every(isNumber);            // true
["1"].every(isNumber);          // false
[1, 2, 3].every(isNumber);      // true
[1, "2", 3].every(isNumber);    // false
[].every(isNumber);             // true
```
- `every()`의 default 반환값은 `true`이고, 콜백 함수가 `false`를 반환할 때에만 `false`를 반환한다.
- 그런데 배연 안에 아이템이 없다면 콜백 함수를 실행할 기회가 없기 때문에 `false`를 반환할 수 없는 것이다.
