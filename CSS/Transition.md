# transition
> [An Interactive Guide to CSS Transitions](https://www.joshwcomeau.com/animation/css-transitions/)

<br/>

## The fundamentals
```css
.btn {
  transition: transform 250ms;
}

.btn:hover {
  transform: translateY(-10px);
}
```
- `transition`은 시간이 지남에 따라 속성이 변경될 때 부드러운 **애니메이션**을 만드는 데 사용된다.
- `transition`에는 두 가지 필수 값이 있다.
  1. 애니메이션을 적용하려는 프로퍼티의 이름
  2. 애니메이션의 지속 시간

<br/>

## Timing functions
### linear
<table>
  <tr>
      <td align="center"><img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/b839142d-3a50-4b5e-a144-d63612694e36"></td>
      <td align="center"><img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/b159accd-1c09-49d0-ab72-4e1b442b302b"></td>
    </tr>
</table>

-  요소가 일정한 속도로, 매 프레임마다 똑같은 양만큼 움직인다.

### ease-out
<table>
  <tr>
      <td align="center"><img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/d3163fb8-0a5f-4590-8041-dc71a2ba4279"></td>
      <td align="center"><img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/ae0c414e-3d6e-4952-966a-fcea3faa6044"></td>
    </tr>
</table>

- 일반적으로 요소가 화면 밖에서 뷰포트에 들어올 때 사용된다. (모달이 표시되는 경우)

### ease-in
<table>
  <tr>
      <td align="center"><img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/413a64f3-e182-49f2-906a-ca72744fb261"></td>
      <td align="center"><img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/7b656070-1201-4ea1-bc50-e2bbb918fb28"></td>
    </tr>
</table>

- 뷰포트 밖으로 사물을 이동하는 경우에 유용하다. (모달이 사라지는 경우)

### ease-in-out
<table>
  <tr>
      <td align="center"><img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/e942d5f8-1cae-4df4-99e2-0f25ba429ffc"></td>
      <td align="center"><img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/3eefd2f5-bc98-445d-8d64-f851fb6e3114"></td>
    </tr>
</table>

- 반복적으로 페이드 인/아웃되는 요소와 같이 루프에서 발생하는 요소에 유용하다.

### ease
<table>
  <tr>
      <td align="center"><img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/57c66349-f150-437d-ba6a-0816bc1c73f5"></td>
      <td align="center"><img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/4163c3d4-7614-436e-b58a-43832d748743"></td>
    </tr>
</table>

- `ease`는 `transition`의 디폴트 값이다.
- 보통 요소가 움직이지만 뷰포트에 들어오거나 나가지는 않는 경우에 사용한다.

### Custom curves
```css
.btn {
  transition:
    transform 250ms cubic-bezier(0.1, 0.2, 0.3, 0.4);
}
```
- 지금까지 살펴본 모든 함수는 `cubic-bezier` 함수에 대한 사전 설정 값이다.
- 2개의 제어점을 나타내는 4개의 숫자 값을 전달한다.

<br/>

## Animation performance
![texture-issue](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/592a9f35-976c-46a3-a1e9-1644ce02273b)

```CSS
.btn {
  will-change: transform;
}
```

- GPU와 CPU는 사물을 렌더링하는 방식이 조금씩 다르기 때문에, 요소 전환 시 CPU가 GPU에 전달하거나 그 반대로 전달할 때 글자가 약간 흔들리는 현상이 발생할 수 있다.
- CSS의 `will-change` 속성은 선택한 요소에 애니메이션을 적용하고 최적화해야 한다는 것을 브라우저에 암시함으로써 이 문제를 해결한다.
- 이 속성은 브라우저가 해당 요소를 항상 GPU가 처리하도록 허용한다는 것을 의미한다.
