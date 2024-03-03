# dialog
```html
<dialog>
  <form method="dialog">
    <h3>This is a pretty dialog</h3>
    <button type="submit">Close</button>
  </form>
</dialog>
```
- `<dialog>` 요소를 통해 커스텀 모달을 생성할 수 있다.

<br/>

```javascript
document.querySelector("button").addEventListener("click", () => {
  document.querySelector("dialog").showModal();
});
```
- `showModal()` 함수를 통해 버튼 클릭 시 모달을 띄운다.

<br/>

## References
- [You don't need JavaScript for that](https://www.htmhell.dev/adventcalendar/2023/2/) / [[번역] 그것을 위해 자바스크립트를 사용할 필요는 없습니다](https://velog.io/@eunbinn/You-dont-need-JavaScript-for-that#%EB%8C%80%ED%99%94-%EC%83%81%EC%9E%90-%EB%AA%A8%EB%8B%AC)
