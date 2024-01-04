# Queueing a Series of State Updates
> [Queueing a Series of State Updates](https://react.dev/learn/queueing-a-series-of-state-updates)

<br/>

## React batches state updates 
```javascript
import { useState } from 'react';

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
- 각 렌더링의 상태 값은 고정되어 있기 때문에 첫 번째 렌더링의 이벤트 핸들러 내부의 `number` 값은 `setNumber(1)`를 몇 번 호출하든 항상 `0`이다.
- 리액트는 상태 업데이트를 처리하기 전에 이벤트 핸들러의 모든 코드가 실행될 때까지 기다린다. 이것이 바로 모든 `setNumber()` 호출이 끝난 후에만 리렌더링되는 이유다.
- 이렇게 하면 여러 컴포넌트에서 여러 상태 변수를 업데이트해도 너무 많은 리렌더링을 실행하지 않고도 업데이트할 수 있다. 하지만 이는 이벤트 핸들러와 그 안의 모든 코드가 완료될 때까지 UI가 업데이트되지 않는다는 의미이기도 하다.
- 리액트는 클릭과 같은 여러 이벤트를 일괄 처리하지 않으며, 각 클릭은 개별적으로 처리된다. `batching`이라고 하는 이 동작은 리액트 앱을 훨씬 빠르게 실행할 수 있게 해준다.

<br/> 

## Updating the same state multiple times before the next render 
- 만약 다음 렌더링 전에 동일한 `state`를 여러 번 업데이트하고 싶다면 `setNumber(number + 1)`처럼 다음 상태 값을 전달하는 대신, `setNumber(n => n + 1)`처럼 `queue`의 이전 상태를 기반으로 다음 상태를 계산하는 함수를 전달할 수 있다.
- 다음 렌더링 중에 `useState`를 호출하면 리액트는 `queue`를 통과한다. `number`의 이전 값은 `0`인데, 리액트는 첫 번째 업데이터 함수에 이 값을 인수 `n`으로 전달한다. 그런 다음 리액트는 이전 업데이터 함수의 반환 값을 가져와서 다음 업데이터에 `n`으로 전달하는 식으로 진행된다.

<br/>

### What happens if you update state after replacing it 
```javascript
<button onClick={() => {
  setNumber(number + 5);
  setNumber(n => n + 1);
}}>
```
1. `setNumber(number + 5)`: `number`는 `0`이므로 `setNumber(0 + 5)`가 된다. 리액트는 "`5`로 바꾸기"를 `queue`에 추가한다.
2. `setNumber(n => n + 1)`: `n => n + 1`은 업데이터 함수다. `n`은 `5`이기 때문에 `setNumber(5 + 1)`가 된다.

<br/>

### What happens if you replace state after updating it 
```javascript
<button onClick={() => {
  setNumber(number + 5);
  setNumber(n => n + 1);
  setNumber(42);
}}>
```
1. `setNumber(number + 5)`: `number`는 `0`이므로 `setNumber(0 + 5)`가 된다. 리액트는 "`5`로 바꾸기"를 `queue`에 추가한다.
2. `setNumber(n => n + 1)`: `n => n + 1`은 업데이터 함수다. `n`은 `5`이기 때문에 `setNumber(5 + 1)`가 된다.
3. `setNumber(42)`: 리액트는 "`42`로 바꾸기"를 `queue`에 추가한다. 리액트는 `42`를 최종 결과로 저장하고 이를 `useState`에서 반환한다.

<br/>

## Recap
- `state`를 설정하는 것이 기존 렌더링의 변수를 변경하지는 않지만 새 렌더링을 요청한다.
- 리액트는 이벤트 핸들러 실행이 완료된 후 상태 업데이트를 처리한다. 이를 `batching`(일괄 처리)라고 한다.
- 하나의 이벤트에서 `state`를 여러 번 업데이트하려면 `setNumber(n => n + 1)`와 같은 업데이터 함수를 사용할 수 있다.


