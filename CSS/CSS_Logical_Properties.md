# CSS Logical Properties
> [Digging Into CSS Logical Properties](https://ishadeed.com/article/css-logical-properties/)

<br/>

## Introduction
![logical-intro-1](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/7e78e120-e311-4d32-87a9-9db7accd3ea8)

- CSS 논리적 속성은 CSS 속성에서 물리적 방향을 사용하지 않고, **HTML 문서의 방향에 따라 달라지는 속성을 사용**한다.
- 상단의 이미지에서 left-to-right(LTR) 레이아웃의 경우 여백은 아바타의 오른쪽에 있고, right-to-left(RTL) 레이아웃의 경우 여백이 왼쪽으로 뒤집혀 있다.

```css
/* without CSS logical properties */
.avatar {
  margin-right: 1rem;
}

html[dir="rtl"] .avatar {
  margin-right: 0;
  margin-left: 1rem;
}

/* with CSS logical properties */
.avatar {
  margin-inline-end: 1rem;
}
```
- CSS 논리적 속성을 사용하면 `margin-inline-end`만 설정함으로써 CSS가 HTML 문서의 방향에 따라 다르게 작동하도록 할 수 있다.

<br/>

## The difference between inline and block
![logical-intro-2](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/f1757e15-af9b-4626-9b39-076635d32da3)

- 쓰기 모드에 따라 `inline` 또는 `block`의 의미가 달라진다.
- 영어와 같은 언어의 경우 `inline`은 가로 차원이고 `block`은 세로 차원이다.
- 반면에 일본어와 같은 언어의 경우 `inline`은 세로 차원이고 `block`은 가로 차원이다.

<br/>

## What does inline mean?
![logical-1](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/497e5fe5-a889-4893-8c97-d0f2e8890366)

- `start`는 LTR 레이아웃(예: 영어)의 경우 왼쪽을, RTL 레이아웃(예: 아랍어)의 경우 오른쪽을 의미한다.
- `end`는 RTL 레이아웃의 경우 왼쪽을, LTR 레이아웃의 경우 오른쪽을 의미한다.

<br/>

## What properties we can use as logical?
대부분의 CSS 프로퍼티는 논리적 프로퍼티로 사용할 수 있다. 
- Sizing: width, height
- Margins, borders, paddings
- Floating, positioning
- Text alignment

<br/>

## Example
![eg-1](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/b868deab-e144-4929-9301-86d8ff4bef0f)

```css
.card {
  padding-inline-start: 2.5rem;
  padding-inline-end: 1rem;
  border-inline-start: 6px solid blue;
}

.card__icon {
  margin-inline-end: 1rem;
}
```
