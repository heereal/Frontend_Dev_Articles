# event.target과 event.currentTarget의 차이점

> The currentTarget read-only property of the Event interface identifies the current target for the event, as the event traverses the DOM.
> **It always refers to the element to which the event handler has been attached, as opposed to Event.target**, which identifies the element on which the event occurred and which may be its descendant.

- `event.target`은 부모로부터 이벤트가 위임되어 발생하는 **내가 클릭한 자식 요소를 반환**한다.
- 하지만 `event.currentTarget`은 **이벤트 핸들러가 부착된 부모의 위치를 반환**한다.

<br/>

```html
<li>
  <button onClick={onLogin}>
    <span>Google</span>
  </button>
</li>
```

<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/28963607-a690-410e-9887-aa81ab34b100" width="500px">

- 버튼을 클릭했을 때 로그를 출력해 보았다.
- `event.target`은 자식 요소인 `span`을 리턴하고, `event.currentTarget`은 부모 요소인 `button`을 반환하는 것을 알 수 있다.

<br/>

## Reference
[JavaScript | event target과 currentTarget의 차이점](https://velog.io/@edie_ko/JavaScript-event-target%EA%B3%BC-currentTarget%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90)
