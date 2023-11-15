# Event Loop

## 자바스크립트와 비동기 처리
- 자바스크립트는 **싱글 스레드** 기반의 언어로, 한 번에 하나의 작업만을 처리할 수 있다. 즉, 자바스크립트 엔진은 **단일 Call Stack**을 사용한다.
- 하지만 실제 자바스크립트가 구동되는 환경(브라우저, NodeJS 등)에서는 주로 여러 개의 스레드가 사용된다.
- 이러한 구동 환경이 단일 Call Stack을 사용하는 자바스크립트 엔진과 상호 연동하기 위해 사용하는 장치가 바로 이벤트 루프인 것이다.

<br/>

## 함수 실행 과정
![gid1 6](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/38e9084b-baf7-4f1e-9c63-e9c1da9db85f)
- `respond` 함수는 `setTimeout` 함수를 반환한다. `setTimeout` 함수는 `Web API`에서 제공되는 함수로, 메인 스레드를 막지 않고 작업을 지연시킬 수 있다.
- `setTimeout`에 전달한 콜백 함수인 화살표 함수 `()=>{return 'Hey'}`가 `Web API`에 추가된다.
- 그동안 `setTimeout` 함수와 `respond` 함수는 그들의 값을 반환했으니, 콜 스택에서 빠져나온다.

<br/>

<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/a660b3a2-81a5-41c0-b10d-e7cccfa15538">

- `Web API` 안에서, 타이머는 `setTimeout`에 전달한 두 번째 인자 `1000ms` 동안 실행된다.

<br/>

![gif3 1](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/a7546824-e8da-4fa9-bb6c-3011b8aacc85)
- **콜백은 즉시 호출 스택에 추가되지 않고, 대신 '큐(대기열)'에 전달**된다. 큐는 대기열이기 때문에, 콜백은 자신의 차례를 기다려야 한다.

<br/>

![gif4](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/81903437-cc49-466b-8450-6c96acb2727b)
- 이제 **이벤트 루프가 큐와 콜 스택을 연결**하는 작업을 수행한다.
- **콜 스택이 비어있다면**, 즉 이전에 호출되었던 모든 함수가 값을 반환하고 콜 스택을 빠져나갔다면, **큐에 있는 첫 번째 요소가 콜 스택에 추가**된다.

<br/>

![gif5](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/ba58ca00-ff28-427d-99a1-6937f98a3c7d)
- 콜백 함수가 콜 스택에 추가되고, 호출되고, 값을 반환하고, 콜 스택을 빠져나간다.

<br/>

## 정리
```javascript
const foo = () => console.log("First");
const bar = () => setTimeout(() => console.log("Second"), 500);
const baz = () => console.log("Third");

bar();
foo();
baz();
```
1. `bar`를 호출해서 `setTimeout`을 반환한다.
2. `setTimeout`에 전달한 콜백은 `Web API`에 추가되고, `setTimeout`, `bar`는 콜스택에서 빠져나온다.
3. 타이머가 실행되고, 그 동안 `foo`가 호출되고 "First"를 기록한다. `foo`는 `undefined`를 반환하고, 1000ms 후에 콜백이 큐에 추가된다.
4. `baz`가 호출되고 "Third"를 기록한다.
5. 이벤트 루프는 `baz`가 값을 반환한 후 콜스택이 비어있음을 확인한다. 그 후 콜백이 콜 스택에 추가된다.
6. 콜백이 실행되며 "Second"를 기록한다.

<br/>

## Reference
- [JavaScript Visualized: Event Loop](https://dev.to/lydiahallie/javascript-visualized-event-loop-3dif) / [[ 번역 ] 자바스크립트 시각화 : 이벤트 루프](https://velog.io/@jjunyjjuny/%EB%B2%88%EC%97%AD-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%8B%9C%EA%B0%81%ED%99%94-%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EB%A3%A8%ED%94%84)
- [자바스크립트와 이벤트루프](https://velog.io/@seungchan__y/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EC%99%80-%EC%9D%B4%EB%B2%A4%ED%8A%B8%EB%A3%A8%ED%94%84#%EF%B8%8F-micro-task--macro-task)
