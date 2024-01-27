# initialData
> [Practical React Query](https://tkdodo.eu/blog/practical-react-query#a-new-cache-entry)

<br/>

```javascript
type State = 'all' | 'open' | 'done'
type Todo = {
  id: number
  state: State
}
type Todos = ReadonlyArray<Todo>

const fetchTodos = async (state: State): Promise<Todos> => {
  const response = await axios.get(`todos/${state}`)
  return response.data
}

export const useTodosQuery = (state: State) =>
  useQuery({
    queryKey: ['todos', state],
    queryFn: () => fetchTodos(state),
    initialData: () => {
      const allTodos = queryClient.getQueryData<Todos>([
        'todos',
        'all',
      ])
      const filteredData =
        allTodos?.filter((todo) => todo.state === state) ?? []

      return filteredData.length > 0 ? filteredData : undefined
    },
  })
```
- 쿼리 키가 캐시의 키로 사용되기 때문에 `state`가 `all`에서 `done`으로 전환될 때 새로운 캐시가 생성되는데, 이로 인해 `state`를 처음으로 전환할 때는 로딩 스피너가 표시될 수 있다.
- 이는 이상적이지 않기 때문에 새로 생성될 캐시 항목을 `initialData`로 미리 채울 수 있다.
- 예시의 경우 클라이언트 사이드에서 사전 필터링을 수행할 수 있다.
- 사용자가 `state`를 전환할 때마다 아직 데이터가 없는 경우 `allTodos` 캐시에서 데이터를 표시하려고 시도한다. 이렇게 하면 사용자에게 `done` 리스트를 즉시 보여줄 수 있으며, 백그라운드에서 fetch가 완료되면 업데이트된 목록을 볼 수 있다.
