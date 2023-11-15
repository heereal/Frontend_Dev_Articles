# Event Loop Task Queue
> [자바스크립트와 이벤트루프](https://velog.io/@seungchan__y/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EC%99%80-%EC%9D%B4%EB%B2%A4%ED%8A%B8%EB%A3%A8%ED%94%84#%EF%B8%8F-%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EB%A3%A8%ED%94%84%EC%99%80-task-queue)

<br/>

## 이벤트 루프와 Task Queue
![image (11)](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/d82d85b0-f361-42a3-bfa0-e6101cecd84a)

- 자바스크립트에서 `Web API`에 정의 되어있는 비동기 이벤트들을 호출하게 되면 `Callback Queue(Task Queue)`와 이벤트 루프가 연계하여 비동기 이벤트를 처리하게 된다.
- `Task Queue`에 의해서 비동기적으로 처리되는 Task들은 크게 두 가지 종류로 나뉜다.
- 우선순위 다소 높은 비동기 API들을 `Macro Task`로 분류하며 대표적인 예로 위에서 다뤘던 `setTimeout`, `setInterval`, `setImmediate` 등이 있다.
- 한편, 이보다 더 높은 우선순위를 가지는 비동기 API들은 `Micro Task`로 분류하며, `Promise` 객체의 `callback`, `queueMicrotask`, `process.nextTick` 등이 있다.

<br/>

![image](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/1a6e3c23-2810-4522-b3d6-5f907e19782a)
- `Micro Task`들이 우선적으로 처리된 이후에, `Macro Task`에 저장된 Task들이 처리되는 모습을 볼 수 있다.
- 물론 `Micro Task`들 역시도 `Call stack`에서 더 이상 처리할게 없어야 비로소 실행된다.

<br/>

## Micro Task , Macro Task 처리 방식 예시
![image (1)](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/1d26e4ed-9e49-47f6-84a5-92757d21f5d4)
- `Call Stack`에 첫 번째 코드 부분이 쌓인 뒤 실행 되어 콘솔창에 `Start!`가 출력된다.

<br/>

![image (2)](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/5a20df53-5936-479e-aee7-f8fa475c634b)
- `setTimeout` 부분이 콜스택에 적재된 이후에 `WebAPI`에 의해 타이머가 작동하게 된다. 0초라서 사실상 바로 타이머는 종료된다.

<br/>

![image (3)](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/76c5872c-edcd-4b39-bb17-d0f75d74af60)
- 타이머가 종료됨에 따라 `setTimeout`의 콜백함수 부분은 `MacroTask`로 분류된다.
- 세 번째 부분인 `Promise`는 `Call Stack`에 적재 된다.
- 이때 `Promise.resolve`는 인자로 받은 값을 `.then` 키워드 부분에 전달하는 역할을 함과 동시에 비동기 처리를 해제하는 역할을 한다. 이에 따라 `.then` 이후 부분은 `MircroTask`에 분류된다.

<br/>

![image (4)](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/5ac35a24-7d65-469f-9b01-a226937b7313)
- 네 번째 부분이 실행됨에 따라 `End!`라는 글자가 콘솔창에 출력된다.
- 이때 `Task Queue`에 적재된 Task들은 아직 `Call Stack` 내부가 비워지지 않음에 따라 Queue에서 빠져나가지 않는다.

<br/>

![image (5)](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/328fff21-94ba-4d39-8dd1-84cd7b0c290b)
![image (6)](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/25c679e3-161f-40b0-b6a6-62e54149ec65)
- `Call stack`이 비워진 것을 파악한 이벤트 루프는 순차적으로 `MicroTask Queue`에 있는 Task들을 비워낸 후 `MacroTask Queue`에 있는 Task들을 비워낸다.
- 비워낼 때에는 `Call Stack`에 적재 시킨 뒤에 순차적으로 실행시켜 처리한다.


