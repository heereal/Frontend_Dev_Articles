# Portals
> [Portal을 활용하여 의미론적 모달 구현하기](https://velog.io/@wuzoo/Portal%EB%A5%BC-%ED%99%9C%EC%9A%A9%ED%95%98%EC%97%AC-%EC%9D%98%EB%AF%B8%EB%A1%A0%EC%A0%81-%EB%AA%A8%EB%8B%AC-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0)
```javascript
ReactDOM.createPortal(child, container)
```
- Portal은 **부모 컴포넌트의 DOM 계층 구조 바깥에 있는 DOM 노드로 자식을 렌더링**하는 최고의 방법을 제공한다.
- 첫 번째 인자는 엘리먼트, 문자열, 혹은 fragment와 같은 어떤 종류이든지 렌더링할 수 있는 React 자식이며, 두 번째 인자는 DOM 엘리먼트이다.
- 예를 들면 `createPortal`를 이용해서 Modal 컴포넌트를 DOM 트리 최상단인 `document.body`에 위치하도록 할 수 있다.
