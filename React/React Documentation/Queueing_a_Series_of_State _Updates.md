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
- 각 렌더링의 상태 값은 고정되어 있으므로 첫 번째 렌더링의 이벤트 핸들러 내부의 숫자 값은 `setNumber(1)`을 몇 번 호출하든 항상 `0`이다.
