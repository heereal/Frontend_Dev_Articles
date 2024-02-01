# Controlled vs. Uncontrolled inputs
> [Using Forms in React](https://daveceddia.com/react-forms/)

<br/>

## Uncontrolled input
- `uncontrolled input`은 더 간단한 입력 방식으로 일반 HTML 입력에 가깝다.
- `uncontrolled input`은 값을 자체적으로 관리한다. 일반 HTML 양식과 마찬가지로 입력 값은 `input`의 `DOM` 노드에 보관되기 때문에 수동으로 추적할 필요가 없다.
- 양식을 제출할 때와 같이 특정 시점에만 입력 값으로 무언가를 수행해야 하는 경우에 적합하다.

<br/>

### Ref
- ref는 DOM 노드에 대한 참조를 보유한다.
- ref는 `JSX`와 실제 `DOM`을 연결하여  리액트 컴포넌트가 이를 표현하는 `DOM` 노드에 접근할 수 있도록 한다.
- `uncontrolled input`에서 입력 값을 가져오려면 참조가 필요한데 이는 `ref` 프로퍼티를 할당함으로써 얻을 수 있다.

<br/>

## Controlled input
- `controlled input`은 입력 값을 명시적으로 제어할 수 있다.
- `controlled input`은 입력 값을 수동으로 관리하기 때문에 값을 유지할 `state`와 변경 핸들러 함수가 필요하다.
- 사용자가 키를 누를 때마다 `state`가 변경되기 때문에 컴포넌트가 리렌더링된다.
- 사용자가 키를 누를 때마다 값을 검사/검증/변환해야 하는 경우에 사용한다.

<br/>

## Is It a Best Practice to Use Controlled Inputs?
- 리액트 문서에는 다음과 같이 `input`에 대한 권장 사항이 있다.
> 대부분의 경우 폼을 구현할 때는 `controlled input`을 사용하는 것이 좋다. `controlled input`에서 폼 데이터는 리액트 컴포넌트에 의해 처리된다. 반면에 `uncontrolled input`은 양식 데이터를 `DOM` 자체에서 처리한다.

