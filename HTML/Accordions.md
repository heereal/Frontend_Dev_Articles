# Accordions
```html
<details open>
  <summary>My accordion</summary>
  <p>My accordion content</p>
</details>
```
- 기본적으로 `details` 요소 안의 모든 내용은 `summary`를 제외하고 숨겨지고, 사용자가 `summary` 요소를 클릭하면 브라우저는 나머지 콘텐츠를 표시한다.
- `open` 속성을 사용하면 아코디언이 처음부터 열려있는 상태로 보여줄 수 있다. `open` 속성은 시작 상태일 뿐이며 사용자가 아코디언과 상호작용할 때마다 업데이트된다.

<br/>

```css
summary::marker {
  font-size: 1.5em;
  content: "📬";
}
[open] summary::marker {
  font-size: 1.5em;
  content: "📭";
}
```
- CSS를 통해 기본적으로 삼각형 형태인 `summery` 요소의 마커를 스타일링 할 수 있다.
  
![image](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/09386ef6-7bee-4b31-9bae-d48bb6895e7a)

<br/>

## References
- [You don't need JavaScript for that](https://www.htmhell.dev/adventcalendar/2023/2/) / [[번역] 그것을 위해 자바스크립트를 사용할 필요는 없습니다](https://velog.io/@eunbinn/You-dont-need-JavaScript-for-that#%EC%95%84%EC%BD%94%EB%94%94%EC%96%B8-%EB%A9%94%EB%89%B4)
