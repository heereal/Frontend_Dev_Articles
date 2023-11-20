# GraphQL

## GraphQL이란?
1. **필요한 데이터만** 한번에, 정확하게 요청한다.
2. **엔드포인트를 통합**한다.
3. **프론트엔드와 백엔드의 커뮤니케이션을 줄이고** 개발에 집중한다.

<br/>

- GraphQL은 Facebook이 개발한 오픈 소스 언어로 현실 세계의 데이터를 표현하는 가장 적합한 방법이 Graph라는 사실에 착안해 개발되었다.
- GraphQL은 API를 위한 **쿼리 언어**이자 서버사이드에서 실행되는 쿼리를 해석하는 **런타임**이다.
- 쿼리 언어는 데이터베이스 또는 데이터 관리 시스템에 접근하기 위한 언어로 대표적으로 SQL을 들 수 있다.
- SQL이 데이터베이스에 질의를 하는 언어인 반면에, GraphQL은 **클라이언트에서 API에게 질의를 하는 언어**이다.

<br/>

![image (10)](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/38331ac2-36d2-4c1b-b490-4384db9b04ef)

- API 사용자는 GraphQL 언어를 사용해서 필요한 데이터를 정확하게 요구하기 위한 텍스트를 구성하고, 클라이언트는 이 텍스트 요청을 전송채널(예:HTTPS)을 통해 API 서비스에 전달한다.
- 그러면 GraphQL Runtime 계층이 이 텍스트 요청을 받아서 백엔드에 있는 다른 서비스들과 커뮤니케이션하고 그 결과들을 모아서 적합한 데이터를 만든다.
- 그렇게 만들어진 데이터를 JSON과 같은 형식으로 API 사용자에게 반환하는 것이다.

<br/>

## REST API vs GraphQL
<img width="921" alt="image (11)" src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/3ed8fd5f-f0e2-430d-b9f0-2213ece382e8">

- REST API는 데이터가 데이터베이스에서 애플리케이션으로 흐르는 인터페이스를 제공한다. 즉, API의 사용자는 서버가 어떤 언어로 만들어져있는지, 데이터베이스는 어떤 것을 쓰는지 신경쓸 필요가 없다.
- REST API는 URL 구조와 쿼리 매개변수를 사용하여 서버에 요청한다. 또한 REST API는 URL과 요청 METHOD를 조합하기 때문에 다양한 Endpoint가 존재한다.
- REST API의 문제점은 다음과 같다.
  - `Overfetching`: REST API의 특성상 데이터를 주고받을 때 클라이언트에서 활용하지 않는 필요 없는 데이터까지 주고받을 확률이 높다. 따라서 이는 불필요한 리소스 낭비를 초래한다.
  - `Underfetching`: 필요한 데이터를 만들기 위해 여러 번의 API 호출이 필요하다.

<br/>

![image (12)](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/1540eee8-5bd0-4880-9e96-5af8efba71e9)

- GraphQL에서는 여러 개의 엔드포인트가 아닌 **하나의 엔드포인트**를 만들고 **한번의 요청으로 원하는 정보만을 얻을 수 있다**. 즉, REST API의 `Overfetching`과 `Underfetching` 문제를 해결할 수 있는 것이다.
- GraphQL은 자신이 선언한 쿼리 내용대로 데이터를 받아올 수 있는 `선언적 data fetching` 구조로 작동한다.
- 따라서 GraphQL의 쿼리와 응답 내용의 구조는 상당히 직관적이다. 요청하는 쿼리문의 구조와 응답의 구조는 거의 일치한다.

<br/>

## Schema
<img width="919" alt="image (13)" src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/4c211257-cf98-4a74-9dc9-7ad6f750a526">

- 이 구조를 GraphQL에서는 스키마(schema)라고 한다.
- 스키마는 타입을 가진 필드를 그래프로 나타낸 것이며 이 그래프는 데이터 서비스를 통해 읽고 수정할 수 있는 모든 객체를 보여준다.
- 따라서 GraphQL 클라이언트는 이 스키마를 통해 서비스에 어떻게 요청할지 알 수 있다.
- 프론트엔드 팀과 백엔드 팀이 스키마를 같이 정의하는 것으로 커뮤니케이션 비용을 줄일 수 있다.

<br/>

## Resolver
- 리졸버 함수는 **어디서 어떻게 데이터를 가져올지 지시**하는 역할을 하며 **스키마의 각 필드는 리졸버 함수와 연동**된다.
- 정리를 하자면 프론트엔드팀과 백엔드팀이 먼저 스키마를 정의한 후 백엔드 팀은 그 데이터를 가져오기 위한 리졸버 함수를 정의한다.
- 이후 클라이언트에서 GraphQL 언어로 텍스트 형태로 필요한 데이터를 요청하면, 백엔드에서 구현된 GraphQL Runtime이 요청을 해석하여 클라이언트가 원하는 데이터를 내려준다.
<br/>

## Reference
- [GraphQL](https://velog.io/@hyunjine/GraphQL)
