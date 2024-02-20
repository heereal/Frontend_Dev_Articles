# Server Side Rendering

## SSR이란?
- **서버에서 HTML 파일을 생성하여 해당 HTML 파일을 클라이언트한테 전송**하는 방식이다.
- 컴포넌트를 렌더링하고 이벤트 핸들러를 붙이는 **Hydration 과정**을 거치면 유저들이 상호작용 할 수 있는 상태가 된다.
- SSR 방식을 통해 사용자들이 자바스크립트가 로드되는 동안 상호작용이 없는 정적 콘텐츠를 더욱 빠르게 볼 수 있다.

<br/>

## SSR이 진행되는 과정
1. 서버에서 전체 앱의 데이터를 fetch한다.
2. 서버에서 전체 앱을 HTML로 렌더링하고 response로 전송한다.
3. 클라이언트에서 전체 앱에 대한 자바스크립트 코드를 로드한다.
4. 클라이언트에서 전체 앱에 대한 자바스크립트 로직을 서버에서 생성된 HTML에 연결한다. (Hydration)
   
<br/>

## `<Suspense>`란?
- React 18에서는 `<Suspense>`를 사용하여 앱을 더 작은 단위로 세분화할 수 있으며, 이러한 단계는 서로 독립적으로 진행되며 **앱의 나머지 부분을 차단하지 않는다**.
- 결과적으로 앱 사용자는 콘텐츠를 더 빨리 확인하고 훨씬 빠르게 상호작용을 시작할 수 있다.

<br/>

## SSR의 문제점
1. **You have to fetch everything before you can show anything**
    - HTML을 렌더하는 시점에 서버에서 컴포넌트 렌더링을 위해 필요한 모든 데이터가 준비되어야 한다.
2. **You have to load everything before you can hydrate anything**
    - Hydration이 시작하기 전에 클라이언트에 모든 컴포넌트에 대한 자바스크립트가 로드되어야 한다.
3. **You have to hydrate everything before you can interact with anything**
    - 서버사이드 렌더링 된 컴포넌트 중 어느 하나라도 상호작용이 가능한 상태가 되기 위해서는 모든 컴포넌트가 Hydration 되어야 한다.

<br/>

## `Suspense`로 SSR의 문제점 보완하기
- React 18의 Suspense를 이용해서 SSR의 모든 과정들이 **Concurrent**하게 이루어지도록 할 수 있다.
  
1. **Streaming HTML before all the data is fetched**
   - 페이지의 일부분을 `<Suspense>`로 감싸서 특정 컴포넌트가 준비되기 전까지 fallback UI (스피너)를 보여주도록 할 수 있다.
   - 예를 들면 `Comments` 컴포넌트를 `<Suspense>`로 감싸줌으로써, 리액트가 페이지의 나머지 부분에 대한 HTML 스트리밍을 시작하기 위해 `Comments` 컴포넌트를 기다릴 필요가 없다는 것을 알려준다.
   - `Comments` 컴포넌트는 초기 HTML 파일에서는 찾아볼 수 없지만, 서버에서 `Comments` 컴포넌트에 대한 데이터가 준비되면 리액트는 동일한 스트림에 추가 HTML을 전송하고, 해당 HTML을 올바른 위치에 배치하기 위한 인라인 `<script>` 태그와 함께 이를 스트리밍한다.
2. **Hydrating the page before all the code has loaded**
   - Selective Hydration을 통해 `<Suspense>`로 감싼 컴포넌트를 제외하고 (해당 컴포넌트가 로드되기 전에) Hydration을 수행할 수 있다.
3. **Hydrating the page before all the HTML has been streamed**
    - 만약 Straming HTML보다도 나머지 부분의 자바스크립트 코드가 더 빨리 로드되었다면 리액트는 나머지 페이지를 먼저 Hydration 한다.
4. **Interactive with the page before all the components have hydrated**
    - Hydration 과정에는 브라우저가 이벤트를 핸들링할 수 있도록 작은 여지(tiny gaps)들이 포함되는데, 예를 들면 유저는 Hydration이 진행되는 동안에도 네이게이션 바를 통해 다른 페이지로 이동할 수 있다.
    - 리액트는 최대한 빨리 모든 것을 Hydration 하면서 **유저의 상호작용을 기반으로** 화면 상에서 **가장 급한 부분에 우선순위를 부여**하여 Hydration 한다.

<br/>

## References
- [New Suspense SSR Architecture in React 18](https://github.com/reactwg/react-18/discussions/37)
- [Suspense SSR Architecture in React 18](https://blog.mathpresso.com/suspense-ssr-architecture-in-react-18-ec75e80eb68d)

