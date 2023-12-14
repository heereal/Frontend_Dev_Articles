# Hoisting

- 자바스크립트 엔진이 스크립트를 전달 받으면 가장 먼저 코드의 데이터에 대한 메모리를 설정한다.
- 이 시점에서는 코드가 실행되는 것은 아니고, 실행을 위한 준비를 하는 것뿐이다.
- 함수의 선언과 변수가 저장되는 방식은 차이가 있다.

<br/>

## Hoisting 시각화

![gif1](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/1fafbed2-e82f-4896-83a7-adc93d094e3b)
1. 함수는 전체 함수에 대한 참조와 함께 저장된다.

<br/>

![gif2](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/1be9f04c-68a1-42ef-b0ca-06b3896a3850)   
2. `let`과 `const` 키워드로 선언되는 변수들은 초기화되지 않는다.

<br/>

![gif3](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/b64f887b-3ccc-44a0-bdd4-8a150525dbdd)   
3. `var` 키워드로 선언된 변수는 `undefined`로 초기화 된 상태로 저장된다.
- 이제 생성 단계가 완료되었기 때문에 코드를 실행할 수 있다.

<br/>

![gif4](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/b715bf56-a436-452f-81c1-6dfe6dd2bf57)   
4. 전체 함수를 참조와 함께 저장했기 때문에, 함수를 선언하기 전에 호출할 수 있다.

<br/>

![gif5](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/e019a5c4-2d66-43b0-b9aa-0d71044a8785)   
5. `var` 키워드로 선언된 변수를 선언 이전에 참조하면 이 변수는 저장된 기본값인 `undefined`를 반환한다.

<br/>

![gif6](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/97758c0f-fd93-441c-a793-6c4a4907ab7c)   
6. 초기화되지 않은 변수를 선언 이전에 참조하면 `ReferenceError`가 발생한다.
- 변수가 실제로 선언된 위치 이전의 영역을 **Temporal Dead Zone**이라고 부른다.
- 초기화되지 않은 변수는 참조할 수 없다.

<br/>

![gif7](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/3b4d4807-5ef5-4c70-a3ac-2465200dd3c2)   
7. 변수가 선언된 해당 라인을 지나가면서, 메모리의 변수를 실제 선언된 값으로 덮어씌운다.

<br/>

## Recap
- 함수와 변수는 해당 코드를 실행하기 전에 실행 컨텍스트를 위 메모리에 저장되는데, 이를 **Hoisting**이라고 한다.
- 함수는 전체 함수에 대한 참조와 함께 저장된다.
- `var` 키워드로 선언된 변수는 `undefined`로 저장되고, `let`과 `const` 키워드로 선언된 변수는 초기화되지 않고 저장된다.

<br/>

## Reference
- [🔥🕺🏼 JavaScript Visualized: Hoisting](https://dev.to/lydiahallie/javascript-visualized-hoisting-478h)
