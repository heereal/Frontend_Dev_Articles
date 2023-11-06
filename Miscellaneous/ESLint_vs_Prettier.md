# ESLint_vs_Prettier
> [ESLint, Prettier Setting, 헤매지 말고 정확히 알고 설정하자.](https://helloinyong.tistory.com/325)   
> "eslint는 코드 퀄리티를 보장하도록 도와주고, prettier는 코드 스타일을 깔끔하게 혹은 통일되도록 도와준다."

<br/>

## ESLint
```javascript
// function 키워드 사용
function foo() {
 ...
}

// arrow function 사용
const foo = () => {
 ...
}
```
- **코드를 일관성 있는 방식으로 작성**할 수 있도록 잡아주는 것이 eslint가 하는 역할이다.

<br/>

## Prettier
```javascript
const foo = () => {
  const a = [1, 2, 3];  // 스코프 내부 작성 시 두 공백 들여쓰기
}
   // <= 빈 줄이 한 줄 이상 안됨.
foo();
```
- prettier는 줄 바꿈, 공백, 들여 쓰기 등 에디터에서 **'텍스트'를 일관되게 작성**하도록 도와준다.
