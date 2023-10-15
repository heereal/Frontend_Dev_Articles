# Sharing State Between Components
> [Sharing State Between Components](https://react.dev/learn/sharing-state-between-components)

<br/>

## 컴포넌트 사이에서 state를 공유하는 방법
1. 자식 컴포넌트에서 state를 없애고, 이 state를 두 컴포넌트의 공통된 부모 컴포넌트로 옮긴다.
2. 부모 컴포넌트의 state를 props 형태로 자식 컴포넌트에 내려준다.
3. 이벤트 핸들러 또한 자식 컴포넌트에 props로 내려 줌으로써 자식 컴포넌트에서 부모 컴포넌트의 state를 수정할 수 있도록 한다.

<br/>

## Controlled components와 Uncontrolled components
- `Controlled components` 컴포넌트가 **props**에 의해 조작된다.
- `Uncontrolled components` 컴포넌트가 **state**에 의해 조작된다.
