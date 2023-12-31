# Bundler
> [번들러란 무엇이며, 어떻게 동작하는 걸까?](https://velog.io/@rookieand/%EB%B2%88%EB%93%A4%EB%9F%AC%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B4%EB%A9%B0-%EC%96%B4%EB%96%BB%EA%B2%8C-%EB%8F%99%EC%9E%91%ED%95%98%EB%8A%94-%EA%B1%B8%EA%B9%8C)

<br/>

## 번들러란 무엇인가?
- 번들러는 여러 개의 Javascript 모듈을 단일 파일로 변환해주는 도구다.

<br/>

## 번들러가 필요한 이유
1. 파일 간의 중복된 식별자 사용으로 인한 **모듈 간 충돌 가능성** 존재
   - 브라우저는 `<script>` 태그를 통해 js 파일을 받는데, Parser의 구조 상 나중에 받은 js 파일의 컨텍스트가 이전에 받았던 js 파일의 컨텍스트를 Override 하기 때문에 문제가 발생한다.
   - 만약에 `hello.js` 와 `world.js`에서 같은 식별자인 word 를 사용한다면 첫 번째로 읽힌 `hello.js` 내에 선언된 변수 word의 값을 먼저 불러오고, 두 번째로 읽힌 `world.js`에서 선언된 변수 word의 값으로 덮어씌워지는 것이다.
2. **다량의 모듈 파일을 전송함**으로써 생기는 딜레이 문제
   - 브라우저에서 웹 애플리케이션을 구축하기 위해 요청을 보내면, 서버에서는 이를 구성하기 위해 필요한 여러 파일을 전송하는데, 이때 구성에 필요한 파일의 갯수가 많아지면 그만큼 요청의 수도 비례하여 증가하므로 응답 시간이 길어진다.

<br/>

## 번들러의 역할
- 번들러는 웹 애플리케이션을 구성하는 **여러 파일을 하나로 묶는 기능**을 하는데, 덕분에 브라우저에서는 각 파일 별로 요청을 보내지 않고 한번의 요청으로 모든 파일을 받을 수 있다.
- 각 모듈 간의 의존성 관계를 파악하여 올바른 순서로 모듈이 불러와지고 실행되는 것을 보장한다.
- 여러 파일을 하나로 합치는 역할 뿐만 아니라, **트랜스파일러 및 컴파일러의 역할**도 겸한다. 예를 들면 트랜스파일러(Babel)로 ES6 기반의 코드를 하위 버전 또는 CJS 기반으로 변환하여 호환성을 지원한다.
- ESM Build를 지원하는 경우, 구조 상 사용되지 않는 모듈을 번들링 결과에 포함시키지 않는 **Tree Shaking**이 적용되어 번들 사이즈를 줄임으로써 사용자에게 더욱 빠른 로딩을 제공한다.

<br/>

## 번들러의 동작 방식
- `Entry File Path`를 기반으로 의존성 관계에 놓인 모듈을 재귀적으로 탐색하고, 각 모듈의 절대 경로를 구하여 **의존성 트리 (Dependency Graph)** 를 구축한다.
- 앞선 과정에서 구축한 의존성 트리를 기반으로 각 모듈을 하나의 번들링 파일로 합쳐 이를 반환한다.
