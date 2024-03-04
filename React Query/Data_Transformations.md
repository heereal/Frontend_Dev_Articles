# 데이터 변환
> [React Query Data Transformations](https://tkdodo.eu/blog/react-query-data-transformations) / [한국어 번역](https://highjoon-dev.vercel.app/blogs/2-react-query-data-transformations)

<br/>

## 1. In the queryFn
```javascript
const fetchTodos = async (): Promise<Todos> => {
  const response = await axios.get('todos')
  const data: Todos = response.data

  // 👇👇
  return data.map((todo) => todo.name.toUpperCase())
}

export const useTodosQuery = () =>
  useQuery({
    queryKey: ['todos'],
    queryFn: fetchTodos,
  })
```
- `queryFn`은 `useQuery`에 전달하는 함수로, `Promise`를 반환해야 하며 결과로 받은 데이터는 쿼리 캐시에 저장된다.
- `queryFn`이 데이터를 반환하기 전에 데이터를 변환할 수 있는데, 이 경우 데이터를 가져올 때마다 데이터 변환도 함께 실행된다.
- 변환된 구조의 데이터는 캐시에 저장되므로 원본 구조에 접근할 수 없다.

<br/>

## 2. In the render function
```javascript
const fetchTodos = async (): Promise<Todos> => {
  const response = await axios.get('todos')
  return response.data
}

export const useTodosQuery = () => {
  const queryInfo = useQuery({
    queryKey: ['todos'],
    queryFn: fetchTodos,
  })

  return {
    ...queryInfo,
    // 👇👇
    data: queryInfo.data?.map((todo) => todo.name.toUpperCase()),
  }
}
```
- 커스텀 훅 내부에서 데이터를 변환할 수도 있다.
- 이 방법을 사용하면 데이터 불러오기 함수가 실행될 때 뿐만 아니라 렌더링 할 때마다 데이터가 변한된다.
- 데이터가 잠재적으로 `undefined`일 수 있으므로 사용할 때 옵셔널 체이닝을 사용하는 것이 좋다.

```javascript
data: React.useMemo(
  () => queryInfo.data?.map((todo) => todo.name.toUpperCase()),
  [queryInfo.data]
),
```
- `useMemo`를 통해 최적화 할 수 있다.

<br/>

## 3. Using the select option
```javascript
export const useTodosQuery = () =>
  useQuery({
    queryKey: ['todos'],
    queryFn: fetchTodos,
    // 👇👇
    select: (data) => data.map((todo) => todo.name.toUpperCase()),
  })
```
- 셀렉터는 `data`가 존재할 때에만 호출되므로 `undefined`를 걱정할 필요가 없다.
- 셀렉터 또한 렌더링 할 때마다 실행된다.
- `useCallback`을 쓰거나 stable 함수 참조로 추출하는 식으로 최적화 할 수 있다.

```javascript
export const useTodosQuery = (select) =>
  useQuery({
    queryKey: ['todos'],
    queryFn: fetchTodos,
    select,
  })

export const useTodosCount = () =>
  useTodosQuery((data) => data.length)
export const useTodo = (id) =>
  useTodosQuery((data) => data.find((todo) => todo.id === id))
```
- select 옵션은 데이터의 일부 항목만 부분적으로 구독하도록 사용할 수도 있다. 

