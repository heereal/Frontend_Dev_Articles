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
