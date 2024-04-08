# React Query Render Optimizations: Tracked Queries
> [React Query Render Optimizations](https://tkdodo.eu/blog/react-query-render-optimizations)

<br/>

## `isFetching` transition
```javascript
{ status: 'success', data: 2, isFetching: true }
{ status: 'success', data: 2, isFetching: false }
```
- 백그라운드 새로고침을 수행할 때마다 컴포넌트는 두 번에 걸쳐 리렌더링된다.
- 만약 로딩 인디케이터를 표시하려는 경우가 아니라면 `isFetching` 정보 때문에 매번 두 번에 걸쳐 리렌더링괴는 것은 불필요할 것이다.

<br/>

## `notifyOnChangeProps`
```javascript
export const useTodosQuery = (select, notifyOnChangeProps) =>
  useQuery({
    queryKey: ['todos'],
    queryFn: fetchTodos,
    select,
    notifyOnChangeProps,
  })
export const useTodosCount = () =>
  useTodosQuery((data) => data.length, ['data'])
```
- 리액트 쿼리에는 `notifyOnChangeProps` 옵션이 있는데, 이 옵션을 `['data']`로 설정하면 옵저버에게 해당 옵션이 변경되는 경우에만 변경 사항을 알리도록 하는 방식으로 렌더링을 최적화 할 수 있다.

<br/>

## Staying in sync
```javascript
export const useTodosCount = () =>
  useTodosQuery((data) => data.length, ['data'])

function TodosCount() {
  // 🚨 we are using error,
  // but we are not getting notified if error changes!
  const { error, data } = useTodosCount()

  return (
    <div>
      {error ? error : null}
      {data ? data : null}
    </div>
  )
}
```
- 하지만 `notifyOnChangeProps` 옵션을 `['data']`로 설정하는 경우, `error`에는 반응하지 않는다거나, `isLoading` 플래그를 사용하고 싶은 경우 등에는 데이터 동기화가 끊어지는 문제가 발생할 것이다.
- 따라서 컴포넌트에서 실제로 사용하는 필드와 `notifyOnChangeProps` 목록을 동기화 상태로 유지할 필요가 있다.
<br/>

## Tracked Queries
```javascript
const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      notifyOnChangeProps: 'tracked',
    },
  },
})
```
- `notifyOnChangeProps`를 `'tracked'`로 설정하면 리액트 쿼리는 **렌더링 중에 사용 중인 필드를 추적하고 이를 사용하여 목록을 계산**한다.
- 추적된 쿼리는 '렌더링 중'에만 작동한다. `useEffect` 중에만 필드에 액세스하는 경우에는 추적되지 않는다.
- v4부터 추적 쿼리는 리액트 쿼리에서 기본적으로 켜져 있으며, `notifyOnChangeProps: 'all'`로 이 기능을 해제할 수 있다.

```javascript
const { isLoading, data } = useQuery(...)
```
- 예를 들면 상단 코드의 경우 리액트 쿼리는 `isLoading`과 `data` 필드를 추적하여 리렌더링을 진행할 것이다.
