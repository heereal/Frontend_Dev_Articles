# React Server Components (RSC)
### React Server Components를 점진적으로 도입하는 방법
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
</br>

> [Everything I wish I knew before moving 50,000 lines of code to React Server Components](https://www.mux.com/blog/what-are-react-server-components)   
> [50,000줄의 코드를 React 서버 컴포넌트로 옮기기 전에 알았더라면 좋았을 것들(번역)](https://ykss.netlify.app/translation/everything_i_wish_i_knew_before_moving_50000_lines_of_code_to_react_server_components/)
- React Server Components의 개념과 장점
- 기존의 코드를 점진적으로 서버 컴포넌트로 migration 하는 방법
