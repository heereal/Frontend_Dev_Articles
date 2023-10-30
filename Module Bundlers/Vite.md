# Vite
> [Is It Time To Say Goodbye To Webpack?](https://gaurav-techgeek.medium.com/time-to-say-goodbye-to-webpack-5bf06ff48823)   
> [(번역) 이제는 웹팩과 작별할 때일까?](https://velog.io/@sehyunny/is-it-time-to-say-goodbye-to-webpack)

<br/>

<img src="https://miro.medium.com/v2/resize:fit:720/format:webp/1*oKe8JQZ1TFzPKAo3ppdkXA.jpeg" width="40%">

## Vite란?
- Vite("빠른" 이라는 의미의 프랑스어)는 오늘날 웹 프로젝트에 더 빠르고 가벼운 개발경험을 제공하는 것을 목적으로 하는 **빌드 도구**이다.
- 매우 빠른 Hot Module Replacement (HMR)와 같이 네이티브 ES모듈을 기반으로 더 향상된 기능을 제공하는 **개발 서버**로서의 역할.
- 프로덕션에 매우 최적화된 정적 에셋을 출력하도록 미리 설정된 Rollup과 함께 코드를 번들링하는 **빌드 명령어**로서의 역할.

<br/>

## Vite가 번들을 분류하는 방법
- **외부 의존성 (Vendor code)**: 외부 의존성은 대부분 개발하는 동안 바뀌지 않는 일반적인 자바스크립트이다. Vite는 esbuild를 이용하여 자바스크립트 기반의 번들러보다 10~100배 빠르게 외부 의존성들을 미리 번들링한다.
- **내부 프로젝트 코드 (ES modules)** : Vite는 네이티브 ESM(ES Module)을 통해 소스 코드를 제공한다. 이는 본질적으로 브라우저에 번들러 작업 일부를 인계하는 것으로서 Vite는 브라우저 요청 시마다 소스 코드를 변환하고 제공하기만 하면 된다.
- 즉, 본질적으로 **서버가 시작되기 전에 코드를 번들링하는 데 시간을 소비하지 않음으로써 개발 서버의 시작 속도를 높인다**는 것을 의미한다.

<br/>

## Hot Module Replacement
- HMR은 나머지 페이지에 영향을 끼치지 않고 특정 모듈만 “hot replace” 하도록 도와준다.
- HTTP 헤더를 활용하여 더 빠르게 리로드하고 캐싱한다.
