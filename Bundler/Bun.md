# Bun
> [Server-Side Rendering (SSR) with Bun and React](https://alexkates.dev/server-side-rendering-ssr-with-bun-and-react)   
> [[번역] 번(Bun)과 리액트로 서버사이드 렌더링(SSR) 구현하기](https://velog.io/@eunbinn/server-side-rendering-ssr-with-bun-and-react)

<br/>

<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/de3f37a5-987e-4531-9989-3306c66df0e2" width="200px">   

## Bun이란?
- 번은 빠른 속도를 위해 설계된 올인원 자바스크립트 런타임 및 툴킷이다.
- 번들러, 테스트 러너, 네이티브 타입스크립트 및 JSX 지원뿐만 아니라 Node.js 호환 패키지 매니저까지 포함되어 있다.

<br/>

## Bun 서버 생성하기
```javascript
const server = Bun.serve({
  port: 3000,
  fetch(req) {
    return new Response(`Bun!`);
  },
});
```
- `const server = Bun.serve({ ... })`: `Bun.serve()`를 사용해 서버를 초기화하고 3000번 포트에서 수신 대기하도록 설정한다.
- `port: 3000`: 서버가 포트 3000에서 수신 대기하도록 지정한다.
- `fetch(req) { ... }`: 들어오는 모든 HTTP 요청을 처리하는 함수를 정의한다. 요청이 들어오면 "Bun!"이라는 텍스트가 포함된 새 HTTP 응답을 반환한다.
- `return new Response(Bun!)`: "Bun!" 텍스트로 새 HTTP 응답 객체를 생성한다.

<br/>

## React와 Bun으로 SSR 구현하기
```javascript
import { renderToReadableStream } from "react-dom/server";
import Pokemon from "./components/Pokemon";

Bun.serve({
  async fetch(request) {

    const stream = await renderToReadableStream(<Pokemon />);

    return new Response(stream, {
      headers: { "Content-Type": "text/html" },
    });
  },
});
```
- `Bun.serve({ ... })`: `Bun.serve()` 메소드를 사용해서 HTTP 서버를 설정한다. 여기에는 들어오는 HTTP 요청을 처리하기 위한 비동기 fetch 함수가 포함되어 있다.
- `async fetch(request) { ... }`: 서버로 들어오는 HTTP 요청에 대해 트리거되는 비동기 함수다.
- `const stream = await renderToReadableStream(<Pokemon />)`: 비동기적으로 `Pokemon` 리액트 컴포넌트를 읽을 수 있는 스트림으로 렌더링한다.
- `return new Response(stream, { ... })`: 읽을 수 있는 스트림이 포함된 새 HTTP 응답 객체를 반환하고 "Content-Type" 헤더를 "text/html"로 설정한다.

<br/>

## 포켓몬을 이용한 동적 라우트 만들기
```javascript
import { PokemonResponse } from "./types/PokemonResponse";
import { PokemonsResponse } from "./types/PokemonsResponse";
import { renderToReadableStream } from "react-dom/server";
import Pokemon from "./components/Pokemon";
import PokemonList from "./components/PokemonList";

Bun.serve({
  async fetch(request) {
    const url = new URL(request.url);

    if (url.pathname === "/pokemon") {
      const response = await fetch("https://pokeapi.co/api/v2/pokemon");

      const { results } = (await response.json()) as PokemonsResponse;

      const stream = await renderToReadableStream(<PokemonList pokemon={results} />);

      return new Response(stream, {
        headers: { "Content-Type": "text/html" },
      });
    }

    const pokemonNameRegex = /^\/pokemon\/([a-zA-Z0-9_-]+)$/;
    const match = url.pathname.match(pokemonNameRegex);

    if (match) {
      const pokemonName = match[1];

      const response = await fetch(`https://pokeapi.co/api/v2/pokemon/${pokemonName}`);

      if (response.status === 404) {
        return new Response("Not Found", { status: 404 });
      }

      const {
        height,
        name,
        weight,
        sprites: { front_default },
      } = (await response.json()) as PokemonResponse;

      const stream = await renderToReadableStream(<Pokemon name={name} height={height} weight={weight} img={front_default} />);

      return new Response(stream, {
        headers: { "Content-Type": "text/html" },
      });
    }

    return new Response("Not Found", { status: 404 });
  },
});
```
- **번으로 HTTP 서버 초기화**: `Bun.serve()` 메서드는 HTTP 서버를 세팅하고 들어오는 비동기 fetch 함수로 모든 HTTP 트래픽의 진입점 역할을 수행한다.
- **모든 포켓몬의 라우트**: URL 경로가 `/pokemon`인 경우 서버는 외부 API에서 포켓몬 목록을 가져와 `PokemonList` 컴포넌트를 HTML로 렌더링한다. 그런 다음 이 HTML은 클라이언트로 다시 전송된다.
- **특정 포켓몬의 라우트**: 이 코드는 정규 표현식을 사용하여 특정 포켓몬의 이름(예: /pokemon/pikachu)을 지정하는 URL 경로를 확인한다. 이러한 경로가 감지되면 서버는 특정 포켓몬에 대한 세부 정보를 가져와서 `Pokemon` 리액트 컴포넌트를 사용하여 렌더링한다.
- **서버 사이드 리액트 렌더링**: 모든 포켓몬 라우트와 특정 포켓몬 라우트 모두에 대해 `renderToReadableStream` 함수는 리액트 컴포넌트를 읽을 수 있는 스트림으로 변환 후 HTML 응답으로 반환한다.
- **에러 핸들링**: 이 코드에는 404 오류에 대한 구체적인 처리 방법이 포함되어 있다. API에서 포켓몬을 찾을 수 없거나 URL이 예상 경로와 일치하지 않는 경우, 404 상태 코드와 함께 "찾을 수 없음" 메시지가 반환된다.







