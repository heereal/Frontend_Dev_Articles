# Suspense
```javascript
const resource = fetchProfileData();

function ProfilePage() {
  return (
    <Suspense fallback={<h1>Loading profile...</h1>}>
      <ProfileDetails />
      <Suspense fallback={<h1>Loading posts...</h1>}>
        <ProfileTimeline />
      </Suspense>
    </Suspense>
  );
}

function ProfileDetails() {
  const user = resource.user.read();
  return <h1>{user.name}</h1>;
}

function ProfileTimeline() {
  const posts = resource.posts.read();
  return (
    <ul>
      {posts.map(post => (
        <li key={post.id}>{post.text}</li>
      ))}
    </ul>
  );
}
```
### 개념
- Suspense는 컴포넌트의 렌더링을 어떤 작업이 끝날 때까지 잠시 중단시키고, 다른 컴포넌트를 먼저 렌더링 할 수 있도록 도와주는 기능
- **Data Fetching 등의 비동기 처리**를 할 때, **응답을 기다리는 동안 fallback UI**(e.g Spinner)를 보여주고, 그 사이에 우선순위가 높은 다른 UI들을 먼저 렌더링 할 수 있다.

<br/>

### Declarative React
- 로딩을 처리하는 부분에 대한 책임과 데이터가 로딩되었는지를 판단하는 책임을 Suspense에 맡기고, 컴포넌트는 정상적으로 데이터가 로딩되었을 때의 UI만 “선언”할 수 있게 된다.

<br/>

### Concurrent React
- 만약 user를 가져오는 API에는 1000ms의 딜레이를 주고, post를 가져오는 API에는 1100ms의 딜레이를 준다면 UserData가 도착한 뒤에 또 다른 1100ms를 기다렸다가 PostData가 로드되는 것이 아니라, **UserData와 PostData가 동시에(정확하게는 Concurrent 하게) 요청되고 이에 따라 1100ms 안에 모든 데이터가 로드**되어 모든 화면이 나타나게 된다.
- 아직 데이터 로딩이 완료되지 않아 Fallback UI를 보여주는 동안에, React는 ‘hidden’ 모드로 Child Component를 렌더 한다. (Render-as-You-Fetch)

<br/>

### 작동 원리
- Suspense가 Fallback UI를 보여주기 위해 사용하는 개념적인 방식은 “promise를 Throw하는 것이다.”
- promise가 throw되면 이 promise가 resolve되기 전까지 Fallback UI를 보여주고 resolve되면, hidden 상태였던 Child Component를 보여준다.

<br/>

### 세 가지 아키텍처에서의 리액트 Suspense
- **Client-side rendering**: `React.lazy`가 로드되는 동안 fallback을 표시한다. Suspense 호환 프레임워크로 데이터를 불러올 때 로딩/오류를 선언적으로 처리한다.
- **Server-side rendering**: 위의 모든 내용 + `<Suspense />`로 감싸진 서버 사이드 렌더링 컴포넌트는 클라이언트에서 우선순위를 부여하여 선택적으로 하이드레이션된다.
- **Server components**: 위의 모든 내용 + `<Suspense />`로 감싸진 비동기 서버 컴포넌트는 단계적으로 클라이언트에서 스트리밍된다. 먼저 fallback, 그 다음 최종 콘텐츠가 스트리밍된다.

<br/>

## reference
> [Conceptual Model of React Suspense](https://blog.mathpresso.com/conceptual-model-of-react-suspense-a7454273f82e)   
> [React Suspense in three different architectures](https://elanmed.dev/blog/suspense-in-different-architectures)   
> [[번역] 세 가지 아키텍처에서의 리액트 Suspense](https://velog.io/@lky5697/suspense-in-different-architectures)

