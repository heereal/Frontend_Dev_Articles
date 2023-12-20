# 기능 구현 아티클 모음
## 상품 상세페이지 더보기
<img src="https://velog.velcdn.com/images/jiwonyyy/post/9ba23590-fe16-4d48-8381-f89a7787ba20/image.png" width="40%">

> [상품 상세페이지 열기/접기 만들기](https://velog.io/@jiwonyyy/%EC%83%81%ED%92%88-%EC%83%81%EC%84%B8%ED%8E%98%EC%9D%B4%EC%A7%80-%EC%97%B4%EA%B8%B0%EC%A0%91%EA%B8%B0-%EB%A7%8C%EB%93%A4%EA%B8%B0)

<br/>

## Next.js SSR 환경에서 다크모드 구현하기
<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/d5a772e8-1bc7-4d3c-8b84-c65ca6f5e39a" width="40%">

> [SSR 환경의 다크모드 깜빡임 현상 해결하기](https://velog.io/@seungchan__y/SSR-%ED%99%98%EA%B2%BD%EC%9D%98-%EB%8B%A4%ED%81%AC%EB%AA%A8%EB%93%9C-%EA%B9%9C%EB%B9%A1%EC%9E%84-%ED%98%84%EC%83%81-%ED%95%B4%EA%B2%B0%ED%95%98%EA%B8%B0#html-blocking)

- Next.js SSR 환경에서 로컬 스토리지와 시스템 설정 값을 활용한 다크모드 구현 코드를 확인할 수 있다.
- 초기 렌더링 시 default 값과 로컬 스토리지에 저장된 유저가 선택한 테마 값이 충돌하여 발생하는 화면 깜박인 현상을 `HTML Blocking`을 통해 해결하였다.
  - `HTML Blocking`은 렌더링 과정 중에 `script` 태그를 만났을 때 HTML 파싱이 중단되는 현상을 의미한다.

<br/>

## 한글 받침에 따라서 은/는 이/가 처리하기
> [한국어 은/는 이/가 와/가 javascript로 처리하기](https://velog.io/@hjkdw95/%ED%95%9C%EA%B5%AD%EC%96%B4-%EC%9D%80%EB%8A%94-%EC%9D%B4%EA%B0%80-%EC%99%80%EA%B0%80-javascript%EB%A1%9C-%EC%B2%98%EB%A6%AC%ED%95%98%EA%B8%B0)
- `charCodeAt` 메소드를 사용해서 문자를 유니코드로 변환한 후 분해하여, 마지막 글자의 종성(받침)에 따라 '와/과'를 구분한다.

<br/>

## SSE(Server Sent Events)로 실시간 채팅 구현하기
> [React와 SSE(Server Sent Events)로 실시간 채팅 구현하기](https://velog.io/@hafnium1923/React%EC%99%80-SSEServer-Sent-Events%EB%A1%9C-%EC%8B%A4%EC%8B%9C%EA%B0%84-%EC%B1%84%ED%8C%85-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0)
- 한 번 연결 요청을 보내면 이벤트가 발생할 때마다 서버에서 응답을 자유롭게 보낼 수 있고, HTTP프로토콜을 이용하기 때문에 훨씬 가볍고 구현 비용이 낮다는 장점으로 SSE를 선택해 실시간 채팅을 구현하였다.

<br/>

## 라이브러리 없이 Toast 만들기
![image](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/24321fe7-99a4-4610-9ba6-224ccc1e2cba)
> [라이브러리 없이 Toast 만들기(feat. TailwindCSS, recoil)](https://velog.io/@pexe99/Boarlog-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC-%EC%97%86%EC%9D%B4-Toast-%EB%A7%8C%EB%93%A4%EA%B8%B0feat.-TailwindCSS-recoil)
- `recoil`과 `TailwindCSS`, `createPortal`을 사용해서 직접 toast를 구현한다.

<br/>

## 카드 Flip 효과 구현하기
![flip](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/fed260f8-0526-4fa1-8db4-d6eb66dc0521)
> [[Boarlog] 아름다운 카드 Flip 효과 구현하기](https://velog.io/@pexe99/Boarlog-%EC%95%84%EB%A6%84%EB%8B%A4%EC%9A%B4-%EC%B9%B4%EB%93%9C-Flip-%ED%9A%A8%EA%B3%BC-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0)
- CSS로 카드를 앞뒤로 뒤집는 애니메이션 효과를 구현한다.
