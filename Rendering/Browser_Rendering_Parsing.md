# Browser Rendering - Parsing
> [브라우저가 읽는 법](https://velog.io/@adultlee/%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80%EA%B0%80-%EB%A5%BC-%EC%9D%BD%EB%8A%94-%EB%B2%95)

<br/>

## 브라우저 렌더링 과정
![image (7)](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/610f0a62-8caa-4f96-8ff7-6b5bff4f92b1)

<br/>

## HTML Parsing
- 브라우저는 `HTML Parser`를 통해서 HTML을 읽어내고, `tag`, `attrivutes`, `content`와 같은 구성 요소를 추출해서 DOM를 생성한다.
- `DOM tree`는 HTML 문서를 파싱하고 이를 의미있는 단위의 집합(Token)으로 변환시킨 뒤, 이를 통해 계층적인 구조를 만들어 낸다.

<br/>

### HTML Parsing Process
![image (9)](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/ddff79e2-6857-44f2-8203-18b60e31bdae)

1. **HTML Token**
- 토큰은 HTML 문서를 구성하는 개별적인 요소를 의미하며 `Tokenization`은 `raw HTML`을 `token`이라고 불리는 더 작은 단위로 분해하는 과정이다.
- `Parsing Algorithm`은 HTML 코드를 분석하며 `token idetification`을 통해서 특정 문자와 순서를 찾아 낸다. 예를 들어서 `<`를 만나면 태그의 시작을 표시하고 이는 토큰의 존재를 의미한다.
-  이 과정에서 HTML 코드는 순차적으로 분석되며 파서가 토큰을 동적으로 식별하는 순간 코드에서 분리한다. 이 과정은 전체 HTML 코드가 토큰화 될 때까지 진행된다.

<br/>

2. **Tokenization Algorithm**
- `Tokenization Algorithm`은 HTML 파싱 과정 중에서 가장 중요한 단계로 파싱 도중 다양한 유형의 토큰을 식별하고 처리하기 위한 논리를 정의한다.
- `Tokenization Algorithm`으로 생성된 토큰들은 DOM을 생성하는 발판이 되어준다.
```html
<!-- Tokenization Example -->
<html> 
  <head>
    <title>My Web Page</title>
  </head>
  <body>
    <p>Welcome to my web page.</p>
  </body>
</html>
```
1. 시작 태그 토큰: `<html>`
2. 시작 태그 토큰: `<head>`
3. 시작 태그 토큰: `<title>`
4. 텍스트 토큰: "My Web Page"
5. 종료 태그 토큰: `</title>`
6. 종료 태그 토큰: `</head>`
7. 시작 태그 토큰: `<body>`
8. 시작 태그 토큰: `<p>`
9. 텍스트 토큰: "Welcome to my web page."
10. 종료 태그 토큰: `</p>`
11. 종료 태그 토큰: `</body>`
12. 종료 태그 토큰: `</html>`

<br/>

3. **Tree Construction**
- HTML 코드가 토큰화 되고 토큰들이 모두 준비가 되었다면, 트리를 구성하는 알고리즘은 이러한 토큰들을 가져와서 `Tree Construction`을 진행하는데 이 과정 중에 DOM이 생성된다.
- DOM Tree를 생성하는 과정
  1. **DOM tree의 root를 생성**: DOM 트리의 계층적 구조를 구성하기 위한 시작점으로 작용한다.
  2. **child Node 생성**: 알고리즘이 토큰화 과정에서 생성된 토큰들을 순회하면서 DOM 트리에 요소 노드를 생성한다. 요소 노드에는 요소의 태그 이름, 속성, 그리고 중첩된 내용이 포함되며 이러한 요소 노드들은 DOM 트리의 구성 요소가 되어, HTML 문서의 구조를 형성한다.
  3. **parent-child relation 생성**: HTML 문서의 계층적 구조를 반영하기 위해 알고리즘은 요소 노드들 사이에 부모-자식 관계를 설정한다. 
  4. **Node간 형제 관계 처리**: 새로운 시작 태그가 이전에 열린 요소와 같은 부모를 공유할 때, 그것은 기존 요소의 형제 관계가 된다.
<br/>

### DOM Tree Construction Example
```html
<html> 
  <head>
    <title>My Web Page</title>
  </head>
  <body>
    <p>Welcome to my web page.</p>
  </body>
</html>
```
```
html
├── head
│   └── title
│       └── "My Web Page"
└── body
    └── p
        └── "Welcome to my web page."
```

<br/>

### 우아한 저하 (Graceful Degradation)
- 우아한 저하 기술을 사용함으로써 알고리즘은 에러가 있더라도 가능한 많은 유효한 콘텐츠를 파싱하고 렌더링하려고 노력한다.
- 따라서 만약 HTML 코드에 문법적 오류가 있더라도 웹 브라우저는 이를 적절히 렌더링하여 사용자에게 의미 있는 콘텐츠를 보여준다.

<br/>

## CSS Parsing
- 브라우저는 `CSS Parsing`을 통해 CSS 코드에서 스타일을 추출하고 저장하여 차후 렌더링 과정에서 활용한다.
- 이렇게 추출된 스타일에는 HTML 요소의 시각적 모양(색, 크기, 모양, 위치 등등)을 결정하는 모든 정보가 포함된다.

<br/>

### CSS Parsing Process
1. **Toknization**
- `Toknization` 과정에서 CSS 코드를 CSSOM의 구성 요소인 개별 토큰으로 나눈다.
- 토큰은 선택자(Selector), 속성(Property), 값(Value), 기호 및 키워드와 같은 고유한 단위를 나타낸다.
```css
/* Tokenization Example */
#main-header {
  font-size: 24px;
  color: blue;
}
```
1. 식별자(Identifier): `#main-header`
2. 여는 중괄호(LeftCurlyBracket): `{`
3. 속성(Property): `font-size`
4. 콜론(Colon): `:`
5. 값(Value): `24px`
6. 세미콜론(Semicolon): `;`
7. 속성(Property): `color`
8. 콜론(Colon): `:`
9. 값(Value): `blue`
10. 세미콜론(Semicolon): `;`
11. 닫는 중괄호(RightCurlyBracket): `}`

<br/>

2. **Lexical Analysis**
- 토큰화된 결과물을 바탕으로 의미 있는 단위로 분해하고 연결하는 작업을 수행한다.

<br/>

3. **Syntax Analysis (구문 분석)**
- `Tokenization` 중에 생성된 토큰을 CSS 구문 규칙에 따라 의미 있는 순서로 정렬하고 구문 규칙을 준수하는지 확인한다.
- 또한 CSS 코드의 계층 구조를 나타내는 `parse tree`을 구축하기 위해 토큰의 배열과 관계를 확인한다.

<br/>

4. **CSS Parsing Algorithm**
- `CSS Parsing Algorithm`은 CSS 규칙이 파싱되고 평가되어 웹 페이지 내의 HTML 요소에 적용되는 체계적인 과정을 정의한다.
-  CSS 규칙을 선택하고 문서 트리의 해당 HTML 요소와 일치하는지 결정한다.
-  부모 요소에서 자식 요소로 스타일을 상속하고 연속 순서를 정해 동일한 요소 간에 충돌을 방지한다.
-  CSS 속성에 대한 최종 속성 값을 계산한다.

<br/>

### CSSOM tree Example
```css
body {
    background-color: #f5f5f5;
}

h1 {
    font-size: 24px;
    color: #333;
}

p {
    font-size: 16px;
    color: #666;
}
```
1. **토큰화**
- `body`, `{`, `background-color`, `:`, `#f5f5f5`, `;`, `}`
- `h1`, `{`, `font-size`, `:`, `24px`, `;`, `color`, `:`, `#333`, `;`, `}`
- `p`, `{`, `font-size`, `:`, `16px`, `;`, `color`, `:`, `#666`, `;`, `}`
2. **구문분석을 통한 parse tree 생성**
```
- STYLESHEET
  - RULESET1
    - SELECTOR: body
    - DECLARATION BLOCK
      - PROPERTY: background-color
      - VALUE: #f5f5f5
  - RULESET2
    - SELECTOR: h1
    - DECLARATION BLOCK
      - PROPERTY: font-size
      - VALUE: 24px
      - PROPERTY: color
      - VALUE: #333
  - RULESET3
    - SELECTOR: p
    - DECLARATION BLOCK
      - PROPERTY: font-size
      - VALUE: 16px
      - PROPERTY: color
      - VALUE: #666
```
3. **CSSOM Tree**

![image (10)](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/5c0ba802-2a11-45f6-b5b2-fdf6d872e9e4)

