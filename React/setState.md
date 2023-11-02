# 왜 setState는 비동기적으로 동작하는가?
> [왜 setState는 비동기적으로 동작하는가?](https://velog.io/@hyunjine/%EC%99%9C-setState%EB%8A%94-%EB%B9%84%EB%8F%99%EA%B8%B0%EC%A0%81%EC%9C%BC%EB%A1%9C-%EB%8F%99%EC%9E%91%ED%95%98%EB%8A%94%EA%B0%80)

<br/>

## setState의 동작 방법
```javascript
export default function App() {
  const [count, setCount] = useState(0);

  const increment = () => {
    setCount(count + 1);
    alert(count);
  };

  return (
    <div className="App">
      <button onClick={increment}>{count}</button>
    </div>
  );
}
```
- 버튼을 누르면 `increment` 함수가 실행되고 차례대로 `setCount(count + 1)`, `alert(count)`가 실행된다.
- 만약 `setCount(count + 1)`이 동기적으로 실행되었다면 `alert(count)`가 출력하는 것은 1이여야 하지만, 결과는 0이 출력된다.
- 즉 `setCount`가 비동기적으로 실행되고 있는 것이다.

<br/>

## 왜 setState는 비동기적으로 작동하는가?
### 1. 내부 일관성 보장(Guaranteeing Internal Consistency)
- 리액트에서 제공하는 객체(state, props, refs)는 내부적으로 서로 일관성이 있으며, **이 객체들은 완전히 조정(reconciled)된 트리를 참조하도록 보장된다**.
- `state`가 동기적으로 업데이트되더라도 `props`는 업데이트되지 않기 때문에, 상위 컴포넌트를 다시 렌더링하기 전에는 `props`를 알 수 없다. 따라서 `state`를 동기적으로 처리하면 일괄 처리(batching)를 할 수 없는 것이다.
- 예를 들어 `state`를 동기적으로 처리했을 때는 `props`는 업데이트되지 않은 상태에서 `state`만 업데이트되는 문제가 발생할 수 있다.

### 2. 동시 업데이트 활성화(Enabling Concurrent Updates)
- 리액트는 "비동기 렌더링"을 통해 이벤트 핸들러, 네트워크 응답, 애니메이션 등의 출처에 따라 `setState()` 호출에 **다른 우선순위를 할당**할 수 있다.
