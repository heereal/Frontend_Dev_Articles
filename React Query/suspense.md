# useQuery의 suspense 옵션
> [React Query에서 'suspense: true' 옵션을 사용했는데도, 'TData' | undefined' 타입이 반환되네요...?!](https://velog.io/@wusi-hub/React-Query%EC%97%90%EC%84%9C-suspense-true-%EC%98%B5%EC%85%98%EC%9D%84-%EC%82%AC%EC%9A%A9%ED%96%88%EB%8A%94%EB%8D%B0%EB%8F%84-TData-undefined-%ED%83%80%EC%9E%85%EC%9D%B4-%EB%B0%98%ED%99%98%EB%90%98%EB%84%A4%EC%9A%94)
```javascript
/// 전역에서 설정
const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      suspense: true,
    },
  },
});

const root = createRoot(document.getElementById("root") as HTMLElement);
root.render(
  <QueryClientProvider client={queryClient}>
    <App />
  </QueryClientProvider>
);

// 각각의 쿼리에서 설정
const { data } = useQuery({ queryKey: ["todos"], queryFn: fetchTodos, suspense: true });
```
- React Query v4에서 suspense 옵션을 사용하면, **useQuery를 리액트의 Suspense와 함께 사용**할 수 있다.
- suspense 옵션은 전역 또는 각각의 쿼리 레벨에서 설정 할 수 있다.
