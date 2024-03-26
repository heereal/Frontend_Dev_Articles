# How To Center a Div
> [How To Center a Div](https://www.joshwcomeau.com/css/center-a-div/?utm_source=oneoneone)

<br/>

## Centering with auto margins
```css
.element {
  max-width: fit-content;
  margin-left: auto;
  margin-right: auto;
}
```
- `fit-content`는 기본적으로 `width`를 `height`처럼 동작하게 하여 요소의 크기가 콘텐츠에 따라 결정되도록 한다.
- `margin-inline: auto;`로 `margin-left`와 `margin-right`을 모두 같은 값인 `auto`로 설정한다.
- 형제 요소를 방해하지 않고 단일 요소를 가로 중앙에 배치하려는 경우에 사용한다.

<br/>

## Centering with Flexbox
```css
.container {
  display: flex;
  justify-content: center;
  align-items: center;
}
```
- 가장 다재다능한 방법으로, 하나 또는 여러 개의 자식을 가로 또는 세로로 가운데에 배치하는 데 사용할 수 있으며, 자식 요소가 포함되거나 넘치거나 상관없이 사용할 수 있다.

<br/>

## Centering within the viewport
```css
.element {
  position: fixed;
  inset: 0px;
  width: 12rem;
  height: 5rem;
  max-width: 100vw;
  max-height: 100dvh;
  margin: auto;
}
```
- `inset: 0px;`은 `top`, `left`, `right`, `bottom`을 모두 같은 값인 `0px`로 설정하는 단축키이다.
- 이 방법의 4가지 핵심 요소는 `position: fixed;`, `inset: 0px;`로 4개의 가장자리에 모두 고정, `width` 및 `height` 고정, ` margin: auto;`이다.
- 사이즈가 정해지지 않은 요소를 뷰포트 중앙에 위치시킬 때는 `width: fit-content; height: fit-content;`를 사용하면 된다.
- 모달이나 배너와 같은 플로팅 UI가 있는 경우에 사용한다.

<br/>

## Centering with CSS Grid
```css
.container {
  display: grid;
  place-content: center;
}
```
- `place-content` 속성은 `justify-content` 및 `align-items`의 줄임말로, 행과 열 모두에 동일한 값을 적용한다.

```css
.container {
  display: grid;
  place-content: center;
  place-items: center;
}
.element {
  grid-row: 1;
  grid-column: 1;
}
```
- 그리드를 이용하면 요소가 모두 동일한 그리드 공간을 공유하도록 지시받기 때문에, 요소 스택을 앞뒤에 겹쳐서 중앙에 배치할 때 사용할 수 있다.
- 모든 요소가 추가되면 그리드의 행과 열은 가장 큰 자식 요소에 맞춰 확장된다.
- 그리드 셀 내에서 이미지를 중앙에 정렬하기 위해 `place-items: center` 속성을 추가했다. `place-items`는 `justify-items`와 `align-items`의 줄임말이다.

<br/>

## Centering text
```css
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
```
- 텍스트 정렬을 위해서는 `text-align`을 사용한다.

