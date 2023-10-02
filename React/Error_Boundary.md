# Error Boundary
> [[React] Error Boundary(에러 바운더리)](https://velog.io/@apro_xo/React-Error-Boundary)
- Error Boundary를 이용해서 리액트에서 에러로 인해 빈 화면을 보여주는 대신 **fallback UI를 보여주는 방식으로 에러를 핸들링**할 수 있다.
- Error Boundary는 클래스형 컴포넌트에서만 사용 가능하며, 함수형 컴포넌트에서 사용하기 위해서는 `react-error-boundary` 패키지를 설치해야 한다.
```javascript
// App.js
import Person from './Person';
import {ErrorBoundary} from 'react-error-boundary';

const ErrorFallback = (err) => {

  console.log(err.error.name);
  console.log(err.error.person_name);
  return(<div>에러났어요@@</div>)
}

function App() {

  return (
    <div className="App">
      <ErrorBoundary FallbackComponent={ErrorFallback}>
      <Person />
      </ErrorBoundary>
    </div>
  );
}

export default App;
// Person.jsx
import React, { useEffect, useState } from "react";
import { useErrorHandler } from 'react-error-boundary';

const Person = () => {
  const person_name = "영희";
  const handleError = useErrorHandler();

  useEffect(() => {
    const getPersonInfo = async () => {
      try {
        const res = await fetch("pata.json", {
          headers: {
            Accept: "application/json",
          },
          method: "GET",
        });
        const data = await res.json()
        console.log(data);
      }
      catch(err) {
        handleError(err);
      }
    };

    getPersonInfo();
  }, []);

  return <div>{person_name}</div>;
};

export default Person;
```
- `react-error-boundary`를 이용해서 에러 발생 시 fallback UI를 지정하거나 에러를 로깅할 수 있다.
