# Recoil
> [Recoil 공식 문서](https://recoiljs.org/ko/docs/introduction/core-concepts)   
> [리액트 상태 관리 라이브러리, 어떤 것을 써야할까?](https://yozm.wishket.com/magazine/detail/2233/?utm_source=oneoneone)

<br/>

## Recoil의 특징
- 리액트 문법 친화적이다. 리액트의 상태처럼 간단한 get/set 인터페이스로 사용할 수 있는 **보일러 플레이트가 없는 API를 제공**한다.
- **비동기 처리**를 추가적인 라이브러리 없이(e.g. redux-thunk, redux-saga) 리코일 안에서 가능하다.
- 내부적으로 **캐싱을 지원**한다. 동일한 atom 값에 대한 내부적으로 메모이제이션된 값을 반환하여 속도가 빠르다.

<br/>

## Atoms 기본 개념
```javascript
const fontSizeState = atom({
  key: 'fontSizeState',
  default: 14,
});

function FontButton() {
  const [fontSize, setFontSize] = useRecoilState(fontSizeState);
  return (
    <button onClick={() => setFontSize((size) => size + 1)} style={{fontSize}}>
      Click to Enlarge
    </button>
  );
}
```
- 아톰(Atoms)은 상태 단위이며, 업데이트와 구독이 가능하다.
- 아톰이 업데이트 됐을 때 해당 아톰을 구독하고 있는 컴포넌트들은 리렌더링이 일어나게 된다.
- 모든 아톰은 전역적으로 고유의 키값을 가져야 하고, 이 키값을 가지고 컴포넌트에서 `useRecoilState`로 불러올 수 있다.

<br/>

## Selectors 기본 개념
```javascript
const fontSizeLabelState = selector({
  key: 'fontSizeLabelState',
  get: ({get}) => {
    const fontSize = get(fontSizeState);
    const unit = 'px';

    return `${fontSize}${unit}`;
  },
});
```
- Selector는 atoms나 다른 selectors를 입력으로 받아들이는 순수 함수(pure function)다.
- 컴포넌트들은 selectors를 atoms처럼 구독할 수 있으며 selectors가 변경되면 컴포넌트들도 다시 렌더링 된다.
- `get` 인자를 통해 atoms와 다른 selectors에 접근할 수 있다. 다른 atoms나 selectors에 접근하면 자동으로 종속 관계가 생성되므로, 참조했던 다른 atoms나 selectors가 업데이트되면 이 함수도 다시 실행된다.

<br/>

## 비동기 데이터 쿼리
```javascript
const currentUserNameQuery = selector({
  key: 'CurrentUserName',
  get: async ({get}) => {
    const response = await myDBQuery({
      userID: get(currentUserIDState),
    });
    return response.name;
  },
});

function CurrentUserInfo() {
  const userName = useRecoilValue(currentUserNameQuery);
  return <div>{userName}</div>;
}
```
- 해당 예제 함수는 `currentUserIDState`에 의존성을 가지고 있는데, 의존성에 변경이 생기면 Selectors는 새로운 쿼리를 다시 실행한다. 그 결과는 쿼리와 유니크한 인풋이 있을 때만 실행되도록 캐시된다.
- 또한 리코일은 비동기 처리 시 프로미스가 resolve 되기 전 보류 중인 경우, 리액트 서스펜스(Suspense)와 함께 동작하도록 디자인되어 있다.
