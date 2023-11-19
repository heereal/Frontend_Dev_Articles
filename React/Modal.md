# React에서 클린한 모달 구현하기
> [클린한 모달 사용하기 - 모달과 컴포넌트의 분리](https://velog.io/@seungchan__y/%ED%81%B4%EB%A6%B0%ED%95%9C-%EB%AA%A8%EB%8B%AC-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0-%EB%AA%A8%EB%8B%AC%EA%B3%BC-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%EC%9D%98-%EB%B6%84%EB%A6%AC)

<br/>

## 기존 모달의 문제점
<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/45d22320-99c6-466d-b781-3660f7a04488" width="80%">

1. **모달 로직으로 인한 코드의 가독성 저하**
    - 렌더링 여부를 담은 상태값, 모달 이벤트 핸들러, 모달 컴포넌트 등 모달을 사용하기 위한 코드들이 뿔뿔이 흩어져 있어 모달의 로직을 파악하기 어렵다.
2. **불필요하게 많은 모달 컴포넌트 렌더링**
    - 만약 댓글마다 댓글 삭제 모달을 추가한다면 모달 컴포넌트가 댓글의 갯수만큼 렌더링된다.

<br/>

## 전역으로 모달 관리하기
- 모달을 사용하는 컴포넌트와 비즈니스 로직 간의 격리
  - 전역에서 모달의 열림/닫힘 상태값를 소유하고 이 값에 따라 모달 컴포넌트를 렌더링 한다.
  - 모달을 띄우는 로직이 필요한 컴포넌트에서 전역단에 선언한 모달 열림/닫힘 상태값을 변경할 수 있도록 한다.
- 여러 개의 모달을 사용할 수 있도록 확장성을 고려한다.
- 필요한 모달 컴포넌트와 그에 대한 정보들을 전역 상태값에 담아두고, 모달을 오픈할 때 모달을 사용하는 컴포넌트에서 모달에 대한 정보를 동적으로 제공하는 방식으로 렌더링한다.

<br/>

## Recoil을 사용한 모달 관리
1. **모달 컴포넌트를 상태값으로 보관하기**
```javascript
import { atom, useRecoilState } from 'recoil';

const modalsAtom = atom({
  key: 'modalsAtom',
  default: [],
});

const useModals = () => {
  const [modals, setModals] = useRecoilState(modalsAtom);

  const openModal = useCallback((Component, props) => {
      setModals((modals) => [...modals, { Component, props: { ...props, open: true } }]);
    },
    [setModals]
  );

  const closeModal = useCallback((Component) => {
      setModals((modals) => modals.filter((modal) => modal.Component !== Component));
    },
    [setModals]
  );

  return {
    modals,
    openModal,
    closeModal,
  };
};
```
- `useModals` 커스텀 훅에서 모달 컴포넌트들을 배열 형태의 상태값으로 보관한다.
- `openModal`에서는 컴포넌트(함수)와 그의 props를 인자로 받아 상태값에 추가한다.

<br/>

2. **상태값으로 보관한 모달들 렌더링하기**
```javascript
import ConfirmModal from '@components/common/ConfirmModal';
import ParticipantsModal from '@components/article/ParticipantModal';

// 사용할 모달 컴포넌트들을 담은 Object
export const modals = {
  confirm: ConfirmModal, 
  participants: ParticipantsModal,
};

const Modals = () => {
  const { modals } = useModals();

  return (
    <>
      {modals.map(({ Component, props }, idx) => {
        return <Component key={idx} {...props} />;
      })}
    </>
  );
};
```
- `modals` 객체 : 모달 컴포넌트들을 담고 있다. 이를 이용해 향후 사용처 컴포넌트에서 모달 컴포넌트들의 코드를 import 하지 않고도 모달의 종류를 선택할 수 있게 도와준다.
- `Modals` 컴포넌트 : `useModals` 훅을 통해 modals 상태값을 받아와 이를 컴포넌트로 렌더링한다.

<br/>

3. **사용처에서 모달 컴포넌트와 로직 넘겨주기**
```javascript
import { modals } from '@components/common/Modals';

const ApplyButton = (...) => {

  const { openModal, closeModal } = useModals();

  return (
    <Button
      onClick={() =>
        openModal(modals.confirm, {
          message: '참가 신청하시겠습니까?',
          onConfirmButtonClick: () => {
    			지원_비즈니스_로직();
			    closeModal(modals.confirm);
		  },
          onCancelButtonClick: () => closeModal(modals.confirm),
        })
      }
    >
      참가하기
    </Button>
  );
};
```
- `openModal` 함수의 인자로 모달 컴포넌트와 그의 props 들을 넘긴다.

<br/>

---

# 효율적인 모달 관리 방법
> [[React] 효율적으로 모달 관리하기](https://leego.tistory.com/entry/React-%ED%9A%A8%EC%9C%A8%EC%A0%81%EC%9C%BC%EB%A1%9C-%EB%AA%A8%EB%8B%AC-%EA%B4%80%EB%A6%AC%ED%95%98%EA%B8%B0)

<br/>

## context API를 사용한 모달 관리
1. **context 생성하기**
```javascript
// context/ModalProvider.js

import React, { useState } from "react";

export const ModalStateContext = React.createContext();
export const ModalSetterContext = React.createContext();

function ModalProvider({ children }) {
  const [state, setState] = useState({
            type: null,
            props: null,
    });

  return (
    <ModalSetterContext.Provider value={setState}>
      <ModalStateContext.Provider value={state}>
        {children}
      </ModalStateContext.Provider>
    </ModalSetterhContext.Provider>
  );
}

export default ModalProvider;
```
-  state와 setter함수 각각의 context를 분리하여 불필요한 리렌더링을 방지한다.

<br/>

2. **Provider로 App 감싸기**
```javascript
// index.js
import ModalProvider from "./context/ModalProvider";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <>
    <ModalProvider>
      <GlobalStyle />
      <App />
      <ModalContainer />
    </ModalProvider>
  </>
);
```
- 생성한 `ModalProvider`로 `App`을 감싸준다.

<br/>

3. **useModal 커스텀 훅 생성하기**
```
// hooks/useModal.js

import { useContext } from "react";
import { ModalSetterContext } from "../context/ModalProvider";

function useModal() {
  const setModalState = useContext(ModalSetterSContext);

  const openModal = ({ type, props = null }) => {
    setModalState({type, props});
  };

  const closeModal = () => {
    setModalState({type: null, props: null});
  };

  return { openModal, closeModal };
}

export default useModal;
```
- `useModal`이라는 커스텀 훅을 생성해서 context를 통해 제공받은 setter 함수를 사용하여 모달을 열고 닫는 로직을 구현하였다.

<br/>

4. **모달 오픈하기**
```javascript
function App() {
  const { openModal } = useModal();

  const onClickButton1 = () => {
    openModal({ type: "first" });
  };

  const onClickButton2 = () => {
    openModal({ type: "second" });
  };

  return (
    <AppWrap>
      <Button onClick={onClickButton1}>Click Me !</Button>
      <Button className="blue" onClick={onClickButton2}>
        Click Me !
      </Button>
        </AppWrap>
    );
}
```
- `useModal`에서 구현한 `openModal` 함수를 사용해서 모달을 띄운다.

<br/>

5. **모달 렌더링하기**
```javascript
// components/ModalContainer.js

import React, { useContext } from "react";
import { createPortal } from "react-dom";
import { ModalStateContext } from "../../context/ModalProvider";
import SampleModal from "./SampleModal";
import SecondModal from "./SecondModal";

const MODAL_COMPONENTS = {
  first: SampleModal,
  second: SecondModal,
};

function ModalContainer() {
  const { type, props } = useContext(ModalStateContext);

  if (!type) {
    return null;
  }

  const Modal = MODAL_COMPONENTS[type];
  return createPortal(
    <>
      <Modal {...props} />
    </>,
    document.getElementById("modal")
  );
}

export default ModalContainer;
```
- 모달 컴포넌트 렌더링을 담당하는 컴포넌트를 생성한다.
- 애플리케이션에서 사용하는 모든 모달 컴포넌트를 `import` 해서 `MODAL_COMPONENTS` 객체에 담아준다.
- `ModalStateContext`로부터 전달받은 `type`에 해당하는 모달 컴포넌트를 렌더링 하고, `props` 값을 넘겨준다.
