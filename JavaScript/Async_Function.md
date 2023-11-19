# 비동기 함수

## 비동기 함수 
- 비동기 함수는 이벤트 루프를 통해 비동기적으로 작동하는 함수로, 암시적으로 **Promise를 사용하여 결과를 반환**한다.

<br/>

## 비동기란?
- 자바스크립트 엔진은 **하나의 실행 컨텍스트 스택**을 가진다. 즉, 자바스크립트에서는 동시에 2개 이상의 함수를 동시에 실행할 수 없다는 뜻이다.
- 이렇게 한 번에 하나의 태스크만 실행할 수 있는 방식을 **싱글 스레드(single thread)** 방식이라고 한다.
- 싱글 스레드 방식에서 처리에 오랜 시간이 걸리는 태스크를 실행할 때 작업이 중단되는 현상을 **블로킹(blocking)** 이라고 한다.

<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/38912fdb-0391-4bb8-bf88-74d8063c1dbd" width="500px">

- `foo` 함수와 `bar` 함수는 `sleep` 함수의 실행이 종료될 때까지 호출되지 못하고 블로킹된다.
- 이와 같이 **현재 실행 중인 태스크가 종료될 때까지 다음 태스크가 대기하는 방식**을 **동기(synchronous) 처리**라고 부른다.

<br/>

<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/bbc4b02b-f2a5-44f5-9016-eb6b4800e5e0" width="500px">

- 반면에 **비동기(asynchronous) 처리**는 **현재 실행 중인 태스크가 종료되기 전에 다음 태스크를 실행**할 수 있다.
- 비동기 처리 방식으로 동작하는 함수를 사용하면 태스크를 블로킹하지 않고 곧바로 실행시킨다.

<br/>

## Promise란?
- `Promise`는 최종 결과를 반환하는 것이 아니라, 미래의 어떤 시점에 결과를 제공하겠다는 '약속'을 반환한다.
- 비유하자면 `async`가 `Promise`라는 포장지로 감싸진 선물을 보낸 것이다. 포장지인 `Promise`를 걷어내고 선물을 얻기 위해 할 수 있는 방법 중 하나가 `await` 사용이다.

<br/>

<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/00be4af1-fad8-40f4-a7cd-8868a169be35" width="500px">

- Promise는 아래 세 가지 중 하나의 상태를 가진다.
  - **대기(pending)**: 비동기 처리가 아직 수행되지 않은 상태
  - **이행(fulfilled)**: 비동기 처리가 성공한 상태
  - **거부(rejected)**: 비동기 처리가 실패한 상태
- 생성 직후의 `Promise`는 `pending` 상태인데, 비동기 처리가 수행되면 상태가 변경된다.
- 비동기 처리에 성공한다면 `resolve` 함수를 호출하고 `fulfilled` 상태가 된다.
- 비동기 처리에 실패한다면 `reject` 함수를 호출하고 `rejected` 상태가 된다.
- 여기서 `resolve`, `reject`는 `Promise`에서 인수로 전달받은 콜백함수이다.
- `fulfilled` 또는 `rejected` 상태를 `settled` 상태라고 한다.
  
<br/>

## await이란?
- `await`는 `Promise`가 `settled` 상태가 될 때까지 대기하다가 `settled` 상태가 되면 `Promise`가 `resolve`한 처리 결과를 반환한다.
- 즉 `await`는 `Promise`의 비동기 처리가 성공 혹은 실패할 때까지 대기하다가, 성공했을 때 `resolve` 함수를 호출한 결과를 반환하고, 실패했을 때 `reject` 함수를 호출한 결과를 반환하는 것이다.

<br/>

## Reference
- [그 async, 꼭 써야 하니?](https://velog.io/@greencloud/%EA%B7%B8-async-%EA%BC%AD-%EC%8D%A8%EC%95%BC-%ED%95%98%EB%8B%88)
