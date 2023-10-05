# Flux
> [Flux](https://velog.io/@hyunjine/Flux)

<br/>

## MVC 패턴의 문제점
<img src="https://velog.velcdn.com/images/hyunjine/post/2513809e-50f6-4548-869a-c7df5d60521c/image.png" width="60%">

- **M**odel, **V**iew, **C**ontroller 영역으로 애플리케이션을 나누고 소프트웨어의 비즈니스 **로직(Model)과 화면(View)을 구분**하는데 중점을 두고 있는 패턴
-  MVC 패턴으로 만들어진 대규모 애플리케이션에서는 데이터가 **양방향**으로 흐르기 때문에 코드의 실행흐름을 추적하는 것이 어렵다.

<br/>

## Flux 패턴
<img src="https://velog.velcdn.com/images/hyunjine/post/16101e46-f633-4902-90f3-b8352fe0a08b/image.png" width="60%">

- Flux는 기존 MVC 모델의 복잡도를 해결하기 위해 설계된 **단방향**의 데이터흐름을 가진 패턴이다.
- **Action**: **상태를 변경하려는 의도를 나타내는 객체**로, Action을 Dispatch하면 Action이 스토어로 전달된다.
- **Dispatcher**: **Action을 Store로 전달**하는 역할을 한다.
- **Store**: **애플리케이션의 전체 상태 트리를 저장**하는 장소다. Dispatcher를 사용해서 전달된 Action을 받고 이를 기반으로 애플리케이션의 상태를 변화시킨다.
- **View**: HTML과 CSS로 만들어지는 결과물(UI)을 의미한다.
- 즉, 애플리케이션에 Action이 들어오면 그 Action을 Store에 Dispatch하고 Store에 데이터가 업데이트되면 View를 리렌더링하는 것이다.
- Flux 패턴에서 변경된 데이터를 감지하여 View에 반영하기 위해서 React 라이브러리를 사용한다.
