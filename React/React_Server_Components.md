# React Server Components (RSC)

## 리액트 서버 컴포넌트란?
- 리액트 서버 컴포넌트는 서버에 위치하기 때문에 네트워크를 통한 데이터 왕복(roundtrips) 없이 서버 인프라에 접근할 수 있다.
- 리액트 서버 컴포넌트를 통해 network waterfalls를 피할 수 있고, 번들 크기를 제로로 줄이기 떄문에 앱의 성능을 향상시킨다.
- 리액트 서버 컴포넌트는 클라이언트 사이드에 접근할 수 없기 때문에 사용자 상호작용을 추가할 수 없다. 예를 들어, 이벤트 핸들러나 `useState`, `useEffect`와 같은 리액트 훅을 사용할 수 없다.
- 서버 컴포넌트는 클라이언트 컴포넌트를 import해서 렌더링할 수 있지만, 반대로는 불가능하다. 그러나 서버 컴포넌트를 클라이언트 컴포넌트에 props로 전달할 수 있다.

<br/>

## 클라이언트 컴포넌트와 서버 컴포넌트를 함께 사용하는 방법
<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/a2391866-ef94-449f-8ac8-b8d6eeb36598" width="400px">

- 컴포넌트 계층 구조의 **루트에 서버 컴포넌트를 배치**하고, **클라이언트 컴포넌트를 컴포넌트 트리의 말단**으로 밀어 넣는 것이 좋다.
- 데이터 불러오기는 서버 컴포넌트의 최상위에서 이루어진다.
- 사용자 상호작용(이벤트 핸들러)과 브라우저 API 액세스는 말단의 클라이언트 컴포넌트에서 처리한다.

<br/>

## React Server Components를 점진적으로 도입하는 방법
<img src="https://cdn.sanity.io/images/2ejqxsnu/production/f7c2ebc75510d0b2618bac342767f81ba7b1e9ed-896x752.png" width="40%"></img>
1. app의 루트에 "use client" 지시문을 추가한다.
2. "use client"를 렌더링 트리에서 가능한 아래로 이동시킨다.
3. 성능 문제가 생긴다면 고급 패턴을 적용한다.

</br>

```javascript
import ClientComponent from './ClientComponent.js'
import ServerComponentB from './ServerComponentB.js'

/** 
  * The first way to mix Client and Server Components
  * is to pass a Server Component to a Client Component
  * as a child.
  */
function ServerComponentA() {
  return (
    <ClientComponent>
      <ServerComponentB />
    </ClientComponent>
  )
}

/** 
  * The second way to mix Client and Server Components
  * is to pass a Server Component to a Client Component
  * as a prop.
  */
function ServerPage() {
  return (
    <ClientComponent
      content={<ServerComponentB />}
    />
  )
}
```
- 클라이언트 컴포넌트에서 import하는 모든 컴포넌트는 클라이언트 컴포넌트가 된다.
- 따라서 서버 컴포넌트를 클라이언트 컴포넌트의 자식 컴포넌트로 만들려면 서버 컴포넌트를 import 하지 말고 **children이나 props로 전달**해야 한다.

</br>

## References
- [Everything I wish I knew before moving 50,000 lines of code to React Server Components](https://www.mux.com/blog/what-are-react-server-components) / [[번역]50,000줄의 코드를 React 서버 컴포넌트로 옮기기 전에 알았더라면 좋았을 것들](https://ykss.netlify.app/translation/everything_i_wish_i_knew_before_moving_50000_lines_of_code_to_react_server_components/)
- [React Server Components – How and Why You Should Use Them in Your Code](https://www.freecodecamp.org/news/how-to-use-react-server-components/) / [[번역] React 서버 컴포넌트를 사용해야 하는 이유와 방법](https://www.freecodecamp.org/korean/news/how-to-use-react-server-components/)
