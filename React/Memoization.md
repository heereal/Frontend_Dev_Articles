# Memoization
> [성능 하면 빠질 수 없는 메모이제이션, 네가 궁금해](https://d2.naver.com/helloworld/9223303)

<br/>

## Memoization이란?
- 메모이제이션은 값비싼 함수 호출의 결과를 **캐싱**하고 동일한 입력이 다시 발생할 때 불필요하게 다시 계산하는 대신 캐싱된 결과를 반환하는 프로그래밍 기술.
- React에서는 `useCallback`, `useMemo`와 같은 Hooks를 통해 성능을 향상시키고 코드의 복잡성을 줄일 수 있다.

<br/>

## Memoization이 필요한 경우
1. **비용이 많이 드는 계산**
2. **자식 컴포넌트에 함수를 props로 넘길 때**
   - 자식 컴포넌트로 전달되거나 이벤트 처리기로 사용되는 콜백 함수가 있는 경우, 콜백 함수를 메모이제이션해 해당 자식 컴포넌트의 불필요한 재렌더링을 방지할 수 있다.
3. **다른 Hook의 의존성에 사용될 때**
   - `useEffect`의 의존성 배열에 비용이 많이 드는 계산이나 렌더링 간에 변경할 필요가 없는 개체가 있는 경우 메모이제이션을 사용할 수 있다.

<br/>

## Memoization이 오히려 성능을 저하시킬 수 있다.
- 하지만 메모이제이션은 메모리에 특정한 값을 저장하는 것이기 때문에, 정말 필요하지 않은 경우에도 남용하면 오히려 성능을 저하시킬 수 있다.
- 일반 함수는 렌더링될 때 기존 함수는 가비지 컬렉션되고 새로운 함수가 생성되는 단순한 작업을 한다.
- 반면, `useCallback`을 사용하면 의존성 확인을 위해 종속된 값들의 참조를 가지고 있어야 하며, 매 렌더링 시마다 해당 값들을 비교해야 한다. 함수 정의를 위해서 배열을 할당해야 하고 이는 메모리에 저장된다.

<br/>

## 메모이제이션은 망가지기 쉽다.
- 컴포넌트가 메모이제이션 되면 React는 각각의 props를 [Object.is](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/is)로 비교한다.
- 하지만 `props`는 렌더링 될 때마다 새로운 객체가 생성되기 때문에 매번 리렌더링된다.
- 컴포넌트가 `children`을 전달받을 때에도 렌더링할 때마다 `React.createElement`로 새로운 객체를 생성하기 때문에 메모이제이션이 의미 없어진다.

<br/>

## Reference
> [성능 하면 빠질 수 없는 메모이제이션, 네가 궁금해](https://d2.naver.com/helloworld/9223303)   
> [The Uphill Battle of Memoization](https://tkdodo.eu/blog/the-uphill-battle-of-memoization) / [[번역] 메모이제이션 고지전](https://velog.io/@cnsrn1874/the-uphill-battle-of-memoization)
