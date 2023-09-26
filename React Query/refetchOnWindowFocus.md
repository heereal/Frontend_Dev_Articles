# refetchOnWindowFocus
> [refetchOnWindowFocus를 무작정 끄시나요?](https://velog.io/@wusi-hub/refetchOnWindowFocus%EB%A5%BC-%EB%AC%B4%EC%9E%91%EC%A0%95-%EB%81%84%EC%8B%9C%EB%82%98%EC%9A%94)
- React Query가 `refetchOnWindowFocus`를 기본적으로 활성화한 이유
  - 리액트 쿼리가 SWR의 caching mechanism을 따르기 때문
- **Stale-While-Revalidate (SWR)** 이란?
  - 웹 애플리케이션에서 데이터를 효율적으로 관리하기 위한 **캐싱 전략**
  - 사용자가 웹 페이지를 열면, 애플리케이션은 데이터를 가져와서 캐시에 저장함
  - 이 데이터는 사용자에게 표시되고, 동시에 서버에 최신 데이터를 요청함
  - 서버로부터 최신 데이터를 받을 때까지 기다리지 않고, 캐시된 데이터를 사용자에게 표시함
- `refetchOnWindowFocus: false` 대신 `staleTime: Infinity`와 `cacheTime: Infinity`를 설정하여 데이터 캐시를 영구화하여 의도치 않은 refetch를 방지할 수 있음
