# Concurrent
## 동시성(Concurrency)이란?
- 리액트에서 동시성을 도입하면서 **여러 작업을 동시에 처리**할 수 있게 되었다.
- 리액트는 작업을 작은 단위로 나눈 뒤 그 **작업들 간의 우선순위를 정하고 그에 따라 작업을 번갈아 수행**한다.
- 작업 간의 전환이 매우 빠르게 이루어지기 때문에 여러 작업이 동시에 수행되는 것 처럼 보이는 것이다.
  
<br/>

## Fetch-on-render
```javascript
function App(){
  return (
      <ArticlePage/>
  );
}

function ArticlePage() {
  const { articles, isLoading } = useArticlesQuery();

  // articles가 로딩되지 않는다면 다른 UI를 보여준다.
  if(isLoading){
    return (
        <Spinner />
    );
  }

  // articles 로딩이 완료되면 해당되는 UI를 보여준다.
  // isLoading이 false가 되기 전까지 TrendArticles는 실행조차 되지 못한다.
  return (
    <>
      {articles.map((article, idx) => <ArticleCard key={idx} article={article}/>}
      <TrendArticles />
    </>
  );
}
```
- **데이터 fetching이 이뤄진 후에 관련된 컴포넌트를 렌더링** 하는 방식이다.
- **Waterfall 현상 발생**: `TrendArticles` 컴포넌트는 `articles` 데이터가 로딩이 완료되어야 렌더링 되기 시작한다. 이러한 `fetch-on-render` 방식이 계층 별로 반복되면 **데이터 fetching도 순차적으로 발생**하기 때문에 렌더링 성능에 나쁜 영향을 끼치게 된다.
- **나쁜 가독성**: 하나의 컴포넌트 코드 내에 로딩 상태에 대한 로직이 포함되어야 한다. 이 때문에 `ArtciePage`에서 핵심로직에 집중하기 어려워진다.

<br/>

## Fetch-then-render
```javascript
function ArticlePage({ ... }) {
  const [allArticles, setAllArticles] = useState([]);
  const [trendArticles, setTrendArticles] = useState([]);

  useEffect(() => {
    // 비동기 작업을 동시에 병렬적으로 실행
    Promise.all([fetchAllArticles(), fetchTrendArticles()]).then(([allArticles, trendArticles]) => {
      setAllArticles(allArticles);
      setTrendArticles(trendArticles);
    });
  }, []);

  return (
    <>
      <AllArticleList articles={allArticles} />
      <TrendArticleList articles={trendArticles} />
    </>
  );
}
```
- `Fetch-on-render` 방식의 Waterfall 현상을 해결할 수 있도록 비동기 **데이터 호출을 `Promise.all`로 묶어 병렬적으로 처리**하는 방법이다.
- **불필요한 관심사들의 결합**: 병렬적으로 처리하는 과정에서 불가피하게 서로 다른 비동기 데이터가 `Promise.all`로 묶이게 된다. 이로 인해 서로 다른 데이터가 하나의 코드에서 호출되게 되며 강한 결합도를 가진다. 만약 `TrendArticles`를 불러오는 부분이 실패하면 `AllArticles` 부분도 렌더링 되지 못할 것이다.
- **다른 비동기 데이터가 완료 되어야 렌더링이 가능** : 가령 `TrendArticles`는 받아올 데이터가 극소수여서 20ms만에 완료되는 한편, `AllArticles`는 받아올 데이터가 너무 많아 100ms 가 소요된다면 `TrendArticles`의 데이터는 빠르게 로드되었음에도 `AllArticles` 때문에 렌더링이 지연된다.

<br/>

## Render-as-you-fetch (with Suspense)
```javascript
function App(){
  return (
  <>
    <Suspense fallback={<Spinner/>}>
      <AllArticlePage/>
    </Suspense>
    <Suspense fallback={<Spinner/>}>
      <TrendArticlesPage/>
    </Suspense>
    ...
  </>;
}

function AllArticlesPage() {
  const { articles } = useArticlesQuery();
  
  return (
    <>
      {articles.map((article, idx) => <ArticleCard key={idx} article={article}/>}
      ...
    </>
  );
}

function TrendArticlesPage() {
  const { articles } = useTrendArticlesQuery();
  
  return (
    <>
      {articles.map((article, idx) => <ArticleCard key={idx} article={article}/>}
      ...
    </>
  );
}
```
- **렌더링 작업과 비동기 데이터 호출 과정이 동시에 이루어진다.**
- 비동기 데이터를 호출하는 과정, fallback UI를 보여주는 과정, 완성된 UI를 보여주는 과정 등 기존의 렌더링 과정들이 여러 작은 태스크들로 쪼개진 뒤 번갈아가며 진행된다.
- 비동기 데이터 호출을 통해 로딩이 발생하면 `Suspense`가 이를 포착하여 fallback UI를 보여주고 로딩이 완료되면 완성된 UI를 보여준다.
- 이를 통해 컴포넌트 내부에선 로딩 상태에 대한 분기 처리가 필요없어져 코드의 가독성이 높아진다.
- 비동기 데이터에 대한 분기처리로 인해 waterfall 현상 역시 사라진다.

<br/>

## tearing 현상이란?
![image](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/c87eaa09-bbfc-4aa7-88cd-0e6a50a7778c)

- tearing은 **UI의 시각적 불일치 현상을 의미**한다.
- 예를 들면 UI의 한 곳에는 스토어가 업데이트되기 이전 값을, 다른 한 곳에서는 스토어가 업데이트된 이후의 값을 표시하는 경우가 있다.
- 자바스크립트는 싱글 스레드이기 때문에 일반적으로 웹 개발에서는 이 문제가 발생하지 않지만 리액트에서는 동시성 기능을 도입하였기 때문에 `startTransition`이나 `Suspense`와 같은 동시성 기능을 사용할 때 Tearing 문제가 발생할 수 있다.

<br/>

```javascript
setInterval(() => {
  dispatch({ type: "increment" });
}, 1000);

function Counter({ index }: { index: number }) {
  const store = useStore();
  const now = performance.now();
  while (performance.now() - now < 500) {
    // 무거운 계산
  }
  
... 생략

function App() {
  const [isOpen, setIsOpen] = React.useState(false);

  return (
    <div className="App">
      <button
        onClick={() =>
          React.startTransition(() => {
            setIsOpen((prev) => !prev);
          })
        }
      >
        {isOpen ? "RESET" : "Tearing 확인하기"}
      </button>
      {isOpen && [...Array(5)].map((_, i) => <Counter key={i} index={i} />)}
    </div>
  );
}
```
1. `setIsOpen`에 의한 렌더링은 `startTransition`으로 감싸져 있으므로 `Concurrent` 하게 렌더링된다. "Tearing 확인하기" 버튼을 누르면 렌더링이 시작된다.
2. `Counter` 컴포넌트가 렌더링되기 시작한다. 하지만 무거운 연산이 내장되어 있기 때문에 천천히 렌더링된다.
3. 이 때 1초가 지나서 `increment` 액션이 디스패치된다. 렌더링을 잠시 멈추고 스토어의 값을 업데이트한다.
4. 렌더링이 다시 시작되고 나머지 `Counter` 컴포넌트를 렌더링한다.
5. 렌더링 중간에 스토어가 업데이트 되었기 때문에 Tearing 현상이 발생한다.

<img width="199" alt="image (1)" src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/fb5a0b2a-5cae-4572-810a-ea4f18479d58"> | ![image (2)](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/4cc2bd67-135d-4e55-aa1b-bc6735044a1b)
--- | --- | 



<br/>

## Reference
- [React 18 Concurrent 로 UX 개선하기](https://velog.io/@seungchan__y/React-18-Concurrent-%EB%A7%9B%EB%B3%B4%EA%B8%B0)
- [React 18 Concurrent Rendering](https://velog.io/@heelieben/React-18-Concurrent-Rendering)
- [리액트에서 외부 시스템과 동기화하기](https://velog.io/@hyunjine/%EB%A6%AC%EC%95%A1%ED%8A%B8%EC%97%90%EC%84%9C-%EC%99%B8%EB%B6%80-%EC%8B%9C%EC%8A%A4%ED%85%9C%EA%B3%BC-%EB%8F%99%EA%B8%B0%ED%99%94%ED%95%98%EA%B8%B0)
