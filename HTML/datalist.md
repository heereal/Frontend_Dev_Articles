# datalist
> [[HTML] datalist와 select 차이점](https://hianna.tistory.com/439)   

```javascript
// datalist 사용 방법
<input list="fruitslist" name="fruits" id="fruits">
<datalist id="fruitslist">
  <option value="apple" label="사과">
  <option value="banana" label="바나나">
  <option value="grape" label="포도">
  <option value="orange" label="오렌지">
</datalist>
```
- `datalist`는 사용자가 입력창에 타이핑을 하면, option 목록에서 일치하는 값을 찾아서 **자동완성** 기능을 제공한다.
- `select`는 사용자가 선택할 수 있는 선택 항목을 제공하고, 그 범위내에서만 선택이 가능하다.
