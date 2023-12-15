# State as a Snapshot
> [State as a Snapshot](https://react.dev/learn/state-as-a-snapshot)

<br/>

## Rendering takes a snapshot in time 
- "렌더링"은 리액트가 함수인 컴포넌트를 호출한다는 것을 의미한다.
- 해당 함수가 반환하는 `JSX`는 해당 시점 UI의 스냅샷과 같다.
- props, 이벤트 핸들러, 지역 변수는 모두 **렌더링 당시의 상태를 사용하여 계산**된다.


<br/>

```javascript
export default function Counter() {
  const [number, setNumber] = useState(0);

  return (
    <>
      <h1>{number}</h1>
      <button onClick={() => {
        setNumber(number + 1);
        setNumber(number + 1);
        setNumber(number + 1);
      }}>+3</button>
    </>
  )
}
```
- `state`는 다음 렌더링에서만 변경된다. 첫 번째 렌더링에서는 `number`가 `0`이다.
- `setNumber(number + 1)`를 세 번 호출하더라도 해당 렌더링 시점 이벤트 핸들러의 `number`는 항상 `0`이기 때문에, `number`를 세 번에 걸쳐 `1`로 변경할 뿐이다.
- 이것이 리액트가 컴포넌트를 리렌더링했을 때 `number`를 `3`이 아닌 `1`로 출력하는 이유다.

<br/>

## State over time 
```javascript
export default function Counter() {
  const [number, setNumber] = useState(0);

  return (
    <>
      <h1>{number}</h1>
      <button onClick={() => {
        setNumber(number + 5);
        setTimeout(() => {
          alert(number);
        }, 3000);
      }}>+5</button>
    </>
  )
}
```
- `setTimeout`을 설정했지만 alert은 여전히 `number`의 초기값인 `0`을 출력한다.
- 리액트에 저장된 `state`가 alert가 실행되는 시점에 변경되었을 수 있지만, 사용자가 사용작용한 시점의 `state` 스냅샷이 사용된다.
- `state`의 값은 이벤트 핸들러가 비동기 함수인 경우에도 렌더링 내에서 변경되지 않는다. 
- `onClick` 함수에서 `setNumber(number + 5)`가 호출된 이후에도 `number`의 값은 여전히 `0`이다.

<br/>

## Recap
- `state`를 변경하면 리렌더링이 발생한다.
- 리액트는 컴포넌트 외부에 `state`를 저장한다.
- `useState`를 호출하면 리액트는 해당 렌더링에 대한 상태 스냅샷을 제공한다.
- 모든 렌더링 및 그 안의 함수는 항상 리액트가 해당 렌더링에 제공한 상태의 스냅샷을 보게 된다.


