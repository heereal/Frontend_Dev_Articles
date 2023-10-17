# useEffect vs useLayoutEffect
> [useEffect 와 useLayoutEffect 의 차이는 무엇일까?](https://medium.com/@jnso5072/react-useeffect-%EC%99%80-uselayouteffect-%EC%9D%98-%EC%B0%A8%EC%9D%B4%EB%8A%94-%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C-e1a13adf1cd5)

<br/>

## 브라우저 렌더링 과정
> DOM 생성 -> CSSOM 생성 -> Render -> Layout -> Paint -> Composite
- **Render**: DOM Tree 를 구성하기 위해 각 엘리먼트의 스타일 속성을 계산하는 과정
- **Paint**: 실제 스크린에 Layout을 표시하고 업데이트하는 과정

<br/>

## useEffect
<img src="https://miro.medium.com/v2/resize:fit:640/format:webp/1*7jCVSsm5-gEoXsgmfGqQyw.png" width="50%">

- `useEffect`는 컴포넌트들이 render 와 paint 된 후 실행된다.
- 비동기적(asynchronous) 으로 실행된다.
- **paint 된 후 실행**되기 때문에 `useEffect` 내부에 dom 에 영향을 주는 코드가 있을 경우 사용자 입장에서는 화면의 깜빡임을 보게 된다.

<br/>

## useLayoutEffect
<img src="https://miro.medium.com/v2/resize:fit:640/format:webp/1*unEeZQLWQrxR93Ao8wBDDg.png" width="50%">

- `useLayoutEffect`는 컴포넌트들이 render 된 후 실행되며, 그 이후에 paint 된다.
- 이 작업은 동기적(synchronous) 으로 실행된다.
- **paint 가 되기전에 실행**되기 때문에 DOM을 조작하는 코드가 존재하더라도 **사용자는 깜빡임을 경험하지 않는다.**

<br/>

> `useLayoutEffect` can hurt performance. Prefer `useEffect` when possible.
- 리액트 공식문서에서는 `useEffect`의 사용을 권장하고 있다.
