# Compound Component Pattern
## Compound Component Pattern이란?
![image (18)](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/e3759b9d-52fc-4ec6-9a2b-ae5ac6d2f697)

- CCP는 **서로 연관된 컴포넌트를 한 파일에 묶은 후에 최상위 컴포넌트에 정적 프로토타입으로 지정하는 방식**을 의미한다.

<br/>

## Compound Component Pattern을 사용하는 이유
1. **재사용성**: 하위 컴포넌트들을 결합하여 하나의 상위 컴포넌트로 만들기 때문에, 각각의 하위 컴포넌트들을 재사용 할 수 있을 뿐만 아니라 상위 컴포넌트도 재사용이 가능해진다.
2. **유연성**: 하위 컴포넌트를 각각 추가하거나 제외시킬 수 있기 때문에 컴포넌트의 형태와 동작을 쉽게 변경할 수 있다.
3. **구조의 명확성**: 상위 컴포넌트와 하위 컴포넌트 간의 관계가 명확해지므로 코드의 가독성을 높이고 유지보수가 용이해진다.
4. **추상화**: 상위 컴포넌트를 통해 컴포넌트의 내부 동작을 추상화하고 숨길 수 있다.

<br/>

## Compound Component Pattern 사용 방법
1. 필요한 하위 컴포넌트들을 모두 import 하기
2. 컴포넌트를 호출할 때 사용할 이름을 정하고 해당 컴포넌트를 할당하기 `상위컴포넌트.호출이름 = 하위컴포넌트;`
3. 필요한 하위 컴포넌트들을 호출해 사용하기

<br/>

```javascript
// 상위 컴포넌트
import AaComponent from "./AaComponent";
import BbComponent from "./BbComponent" ;
import CcComponent from "./CcComponent ";

export default function CompoundComponent({children}: {children: ReactNode}) {
  return (
    <div>{children}</div>
  );
}

CompoundComponent.Aa = AaComponent;
CompoundComponent.Bb = BbComponent;
CompoundComponent.Cc = CcComponent;

// 컴포넌트 사용
import CompoundComponent from "./component/CompoundComponent"

function App() {
  return (
    <CompoundComponent>
      <CompoundComponent.Aa />
      <CompoundComponent.Bb />
      <CompoundComponent.Cc />
    </CompoundComponent>
  );
}
```
- 이제 `CompoundComponent`가 필요한 곳이라면 하위 컴포넌트들을 일일이 import 하지 않고 상위 컴포넌트 하나만 import 하면 모든 하위 컴포넌트들을 호출할 수 있다.
- `CompoundComponent`를 다른 곳에서 재사용 할 때 위 컴포넌트인 `Aa` , `Bb` , `Cc` 컴포넌트 중 일부만 사용하고 싶은 경우에도 간단하게 구현할 수 있다.
  
<br/>

## Compound Component Pattern 코드 예시
```javascript
const FlyOutContext = createContext();

function FlyOut(props) {
  const [open, toggle] = useState(false);

  return (
    <FlyOutContext.Provider value={{ open, toggle }}>
      {props.children}
    </FlyOutContext.Provider>
  );
}
```
- `FlyOut` 컴포넌트는 상태를 보유하고, 모든 자식 컴포넌트에게 토글 값이 포함된 `FlyOutProvider`를 반환한다.

<br/>

```javascript
const FlyOutContext = createContext();

function FlyOut(props) {
  const [open, toggle] = useState(false);

  return (
    <FlyOutContext.Provider value={{ open, toggle }}>
      {props.children}
    </FlyOutContext.Provider>
  );
}

function Toggle() {
  const { open, toggle } = useContext(FlyOutContext);

  return (
    <div onClick={() => toggle(!open)}>
      <Icon />
    </div>
  );
}

function List({ children }) {
  const { open } = useContext(FlyOutContext);
  return open && <ul>{children}</ul>;
}

function Item({ children }) {
  return <li>{children}</li>;
}

FlyOut.Toggle = Toggle;
FlyOut.List = List;
FlyOut.Item = Item;
```
- `Toggle`, `List`, `Item` 컴포넌트를 `FlyOut` 컴포넌트의 프로퍼티로 만든다.
- 즉, 어떤 파일에서든 `FlyOut` 컴포넌트를 사용하려면 `FlyOut` 컴포넌트만 import하면 된다.

<br/>

```javascript
import React from "react";
import { FlyOut } from "./FlyOut";

export default function FlyoutMenu() {
  return (
    <FlyOut>
      <FlyOut.Toggle />
      <FlyOut.List>
        <FlyOut.Item>Edit</FlyOut.Item>
        <FlyOut.Item>Delete</FlyOut.Item>
      </FlyOut.List>
    </FlyOut>
  );
}
```
- 최종적으로 `FlyoutMenu` 컴포넌트 자체에 상태를 추가하지 않고도 `FlyOut` 컴포넌트 전체를 생성했다.

<br/>

## Compound Component Pattern의 단점
1. **학습 곡선**: 리액트에 대한 이해가 부족하다면 CCP를 적용하기 힘들 수 있고, 리액트 사용에 능숙하다고 해도 아무런 학습 없이 바로 CCP를 적용할 수는 없다.
2. **너무나도 많은 유연성**: CCP는 쉽게 구조를 변경할 수 있어서 유연성이 좋은 편이지만 이것이 처음 CCP를 적용한 개발자의 의도가 아닌 전혀 다른 방식으로 컴포넌트를 사용하는 상황이 발생할 가능성도 존재한다.
3. **테스트의 어려움**: CCP는 단일 컴포넌트보다 많은 컴포넌트로 구성되어 있기 때문에 단위 테스트를 작성할 때 까다로울 수 있다.

<br/>

## References
- [React Compound 패턴 적용하기](https://velog.io/@junhopportunity/React-Compound-%ED%8C%A8%ED%84%B4-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0)
- [Compound Pattern](https://www.patterns.dev/react/compound-pattern/)
