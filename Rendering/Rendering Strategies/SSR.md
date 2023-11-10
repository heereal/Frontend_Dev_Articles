## Server Side Rendering
### SSR이란?
- 서버에서 HTML 파일을 미리 준비하여 클라이언트한테 응답해주는 방식
- React가 로드되고 나서 컴포넌트를 메모리에 렌더링하고 이벤트 핸들러를 붙이는 **Hydration 과정**을 거치면 유저들이 interactive 할 수 있는 상태가 된다.
- SSR 방식이 애플리케이션의 상호작용을 더 빠르게 만들지는 않지만, 유저들이 자바스크립트가 로드되는 동안 상호작용이 없는(non-interactive version) 정적 콘텐츠를 더 빠르게 볼 수 있도록 해준다.

<br/>

### SSR의 문제점
1. **You have to fetch everything before you can show anything**
    - HTML을 렌더하는 시점에 서버에서 컴포넌트 렌더를 위해 필요한 모든 데이터가 준비되어야 한다.
2. **You have to load everything before you can hydrate anything**
    - Hydration이 시작하기 전에 클라이언트에 모든 컴포넌트에 대한 자바스크립트가 로드되어야 한다.
3. **You have to hydrate everything before you can interact with anything**
    - 서버사이드 렌더 된 컴포넌트 중 어느 하나라도 상호작용이 가능한 상태가 되기 위해서는 모든 컴포넌트가 Hydration 되어야 한다.

<br/>

### Suspens로 SSR의 문제점 보완하기
- React 18의 Suspense를 이용해서 SSR의 모든 과정들이 “Concurrent” 하게 이루어지도록 할 수 있다.
1. **Streaming HTML before all the data is fetched**
   - 페이지의 부분을 Suspense로 감싸서 특정 컴포넌트가 준비되기 전까지 fallback UI를 보여주도록 할 수 있다.
   - 예를 들면 “Comments” 컴포넌트를 “Suspense”로 감싸줌으로써, “Comments” 컴포넌트를 기다리지 말고 우선 나머지 페이지에 대해서 HTML을 Streaming 할 수 있도록 한다.
2. **Hydrating the page before all the code has loaded**
   - Selective Hydration을 통해 Suspense로 감싼 컴포넌트를 제외하고(해당 컴포넌트가 로드되기 전에) Hydration을 수행할 수 있다.
3. **Hydrating the page before all the HTML has been streamed**
    - 만약 Straming HTML보다도 나머지 부분의 자바스크립트 코드가 더 빨리 로드되었다면 리액트는 나머지 페이지를 먼저 Hydration 한다.
    - Suspense는 일관적으로 non-blocking 하게 동작하며, 리액트는 그저 먼저 도착한 것을 먼저 처리할 뿐이다.
4. **Interactive with the page before all the components have hydrated**
    - Hydration 과정에는 브라우저가 이벤트를 핸들링할 수 있도록 작은 여지(tiny gaps)들이 포함되는데, 예를 들면 유저는 Hydration이 진행되는 동안에도 네이게이션 바를 통해 다른 페이지로 이동할 수 있다.
    - 리액트는 최대한 빨리 모든 것을 Hydration 하면서 유저의 상호작용을 기반으로 화면 상에서 가장 급한 부분에 우선순위를 부여하여 Hydration 한다.

<br/>

> [Suspense SSR Architecture in React 18](https://blog.mathpresso.com/suspense-ssr-architecture-in-react-18-ec75e80eb68d)
- React 18의 Suspense가 SSR의 문제점을 어떻게 보완했는지
