# Inside React Query
> [Inside React Query](https://tkdodo.eu/blog/inside-react-query)   
> [[번역] Inside React Query](https://velog.io/@hyunjine/Inside-React-Query)

<br/>

## The QueryClient
![image (9)](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/86a6be54-cb8b-42f5-ba13-56e9b922ac16)

```javascript
import { QueryClient, QueryClientProvider } from '@tanstack/react-query'

// ⬇️ this creates the client
const queryClient = new QueryClient()

function App() {
  return (
    // ⬇️ this distributes the client
    <QueryClientProvider client={queryClient}>
      <RestOfYourApp />
    </QueryClientProvider>
  )
}
```
- `QueryClient`는 애플리케이션 시작 시 인스턴스를 생성한 다음 `QueryClientProvider`를 통해 어디에서나 사용할 수 있다.
- `QueryClientProvider`는 `React Context`를 사용해서 `QueryClient`를 애플리케이션 전체에 배포한다.
- `client`는 단 한 번 생성되기 때문에 리렌더링되지 않으며, `useQueryClient`를 통해 `client`에 대한 접근을 허용할 뿐이다.
- `QueryClient`는 `new QueryClient`를 생성할 때 자동으로 생성되는 `QueryCache`와 `MutationCache`를 담는 컨테이너로서의 역할을 한다.
- 또한 모든 `query` 및 `mutation`에 대해 설정할 수 있는 몇 가지 기본값을 보유하고 있으며 캐시 작업을 위한 편리한 방법을 제공한다. 대부분의 경우 캐시와 직접 상호작용하지 않고 `QueryClient`를 통해 캐시에 접근한다.

<br/>

## QueryCache
![image (10)](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/038f1731-fb55-4f4c-8119-eebf831b1637)
- `QueryCache`는 키는 안정적으로 직렬화된 `queryKeys`의 버전(`queryKeyHash`라고 부름)이고, 값은 `Query` 클래스의 인스턴스인 in-memory 객체다.
- `React Query`는 기본적으로 메모리에만 데이터를 저장하고 다른 곳에는 저장하지 않는다는 것을 이해하는 것이 중요하다.
- 브라우저 페이지를 새로고침하면 캐시는 사라질 것이다. 만약 로컬 스토리지와 같은 외부 저장소에 캐시를 작성하고 싶다면 `persisters`를 살펴보자.

<br/>

## Query
<img alt="query" src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/8d95dda0-d81d-4368-bcc2-f9774afc2d5d">

- 캐시에는 쿼리들이 있으며 `Query`는 대부분의 로직이 발생하는 곳이다.
- `Query`는 쿼리에 대한 모든 정보(데이터, 상태 필드, 메타 정보)를 포함하고 있을 뿐만 아니라, 쿼리 함수를 실행하고 재시도, 취소, 중복 제거와 같은 로직들을 포함하고 있다.
- `Query`는 누가 쿼리 데이터에 관심이 있는지 알고 있으며 이에 대한 모든 변동사항을 `Observer`에 전달한다.

<br/>

## QueryObserver
<img alt="queryObserver" src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/75cb378c-4662-4ae8-bd3b-7efb3e9642fe">

- `Observer`는 `Query`와 이를 사용하는 컴포넌트 사이에 접착제 역할을 한다.
- `Observer`는 `useQuery`를 호출할 때 생성되며, 오로지 하나의 쿼리만을 구독한다. 그렇기 때문에 `useQuery`에 `queryKey`를 전달해야 하는 것이다.
- `Observer`는 컴포넌트가 `Query`의 어느 속성을 사용하는지 알기 떄문에 관련되지 않은 변경사항은 알리지 않는다.
- 예를 들어 데이터 필드만을 사용한다면, 백그라운드 refetch에서 `isFetching`이 변경되는 경우 컴포넌트를 리렌더링할 필요가 없을 것이다.

<br/>

## Active and inactive Queries
<img width="137" alt="devtools" src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/8fd725d2-cc9f-4bdc-930d-8ee99d6b5b71">

- `Observer`가 없는 쿼리를 비활성 쿼리라고 한다. 여전히 캐시에 있지만 어떤 컴포넌트에서도 사용되지 않고 있다.
- React Query Devtools를 살펴보면 비활성 쿼리가 회색으로 표시되는 것을 볼 수 있다. 왼쪽의 숫자는 쿼리를 구독하는 `Observer`의 수를 나타낸다.

<br/>

## The complete architecture
<img alt="architecture" src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/6ad74c1b-7323-4c4b-a7d6-25cf88175a9c">

- 대부분의 로직이 프레임워크에 구애받지 않는 `Query Core` 내부에 있음을 알 수 있다.

<br/>

## From a component perspective
<img alt="flow" src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/faa49c28-99af-42f3-bbd2-aadfc30f19dc">

1. 컴포넌트가 마운트되면 `Observer`를 생성하는 `useQuery`를 호출한다.
2. `Observer`는 `QueryCache`에 있는 `Query`를 구독한다.
3. 해당 구독은 `Query`가 아직 존재하지 않는 경우 `Query` 생성을 트리거하거나, 데이터가 오래된 것으로 간주되는 경우 백그라운드에서 `fetching`을 트리거할 수 있다.
4. `fetching`을 시작하면 `Query`의 상태가 변경되므로 `Observer`에 이에 대한 정보가 제공된다.
5. `Observer`는 몇 가지 최적화를 실행하고, 컴포넌트에 잠재적인 업데이트 사항을 알림으로써 새 상태를 렌더링할 수 있도록 한다.
6. `Query`의 실행이 종료면 `Observer`에게도 이 사실을 알린다.
- 모든 흐름에서 동일한 점은 대부분의 로직이 리액트 외부에서 발생하며, 상태 시스템의 모든 업데이트가 `Observer`에 전달되어 컴포넌트에도 이를 전달해야 하는지를 `Observer`가  결정한다는 점이다.

