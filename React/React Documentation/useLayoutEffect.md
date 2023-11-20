# useLayoutEffect
> [useLayoutEffect](https://react.dev/reference/react/useLayoutEffect)

<br/>

## useLayoutEffect란?
```javascript
useLayoutEffect(setup, dependencies?)
```
- `useLayoutEffect`는 브라우저가 화면을 `repaint`하기 전에 실행되는 `useEffect`의 버전이다.
- 해당 컴포넌트가 DOM에 추가되기 전에 `setup` 함수가 실행된다.
- `useLayoutEffect`는 클라이언트에서만 실행된다. 서버 렌더링에서는 사용할 수 없다.
- `useLayoutEffect` 내부의 코드가 실행되는 동안 브라우저가 화면을 `repaint`하는 것을 차단한다. 이를 과도하게 사용할 경우 앱의 성능에 영향을 미칠 수 있기 때문에 가능하면 `useEffect`를 사용하는 것을 추천한다.

<br/>

## 사용 예시
```javascript
function Tooltip() {
  const ref = useRef(null);
  const [tooltipHeight, setTooltipHeight] = useState(0); // You don't know real height yet

  useLayoutEffect(() => {
    const { height } = ref.current.getBoundingClientRect();
    setTooltipHeight(height); // Re-render now that you know the real height
  }, []);

  // ...use tooltipHeight in the rendering logic below...
}
```
브라우저가 화면을 `repaint`하기 전에 레이아웃을 측정하기 위해 `useLayoutEffect`을 사용할 수 있다.
1. `Tooltip`이 `tooltipHeight = 0`이라는 초기값과 함께 렌더링된다.
2. 리액트는 이를 DOM에 위치시키고 `useLayoutEffect` 내부의 코드를 실행한다.
3. `useLayoutEffect`가 툴팁 내용의 높이를 측정하고 즉시 리렌더링을 유발한다.
4. `tooltipHeight`의 실제 높이를 이용해 `Tooltip`이 리렌더링된다.
5. 리액트가 이를 DOM에서 업데이트하고, 브라우저는 최종적으로 툴팁을 보여준다.   

중요한 점은 툴팁의 높이가 초기값 0에서 실제 측정된 높이로 두 단계에 거쳐 렌더링되더라도 사용자에게는 오직 최종 결과만 보여진다는 것이다.

