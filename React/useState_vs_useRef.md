# useState vs useRef
> [useState vs useRef](https://velog.io/@hyunjine/useState-vs-useRef)

<br/>

## useState
```javascript
const [state, setState] = useState(initialState);
```
- `useState`로 state를 변경할 경우 컴포넌트가 **리렌더링**된다.

<br/>

## useRef
```javascript
function Component (props) {
  const textInput = useRef(null);

  function handleClick() {
    textInput.current.focus();
  }

  return (
    <div>
      <input type="text"ref={textInput} />
      <button onClick={handleClick}>click me</button>
    </div>
  );
}
```
- `useRef`는 render 메서드에서 생성된 **DOM 노드나 React 엘리먼트에 접근**하는 방법을 제공한다.
- React 공식 문서에 의하면 ref의 바람직한 사용 사례는 다음과 같다.
  - 포커스, 텍스트 선택영역, 혹은 미디어의 재생을 관리할 때
  - 애니메이션을 직접적으로 실행시킬 때
  - 서드 파티 DOM 라이브러리를 React와 같이 사용할 때

<br/>

## Controlled Components vs Uncontrolled Components
- `Controlled Components` useState에 의해 상태로 관리하고 있는 컴포넌트.
- `Uncontrolled Components` React가 상태로 추적하고 있지 않은 컴포넌트. ref를 활용해 실제 DOM에 접근하며 DOM자체에서 데이터가 다뤄진다.
- **실제 DOM에 접근해야하는 상황이 아니라면 React 컴포넌트가 input의 상태를 관리하는 것을 추천**한다. (Controlled Components)



