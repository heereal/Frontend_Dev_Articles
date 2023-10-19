# 웹 폰트
> [웹 폰트 사용 가이드](https://velog.io/@ken1204/%EC%9B%B9-%ED%8F%B0%ED%8A%B8-%EC%82%AC%EC%9A%A9-%EA%B0%80%EC%9D%B4%EB%93%9C)

<br/>

## 웹 폰트 렌더링 과정의 문제점
- CSSOM(CSS Object Model)을 생성하는 과정에서 외부 웹 폰트 링크로 정의된 부분을 만나고 해당 폰트 파일을 다운로드하기 시작한다.
- **Paint 단계에서 웹 폰트 파일처럼 외부 링크로 연결된 파일의 다운로드가 완료되지 않았으면 브라우저는 해당 자원을 사용하는 콘텐츠의 렌더링을 차단**한다.
- 따라서 렌더링이 차단되는 현상을 방지하기 위해 폰트의 로드 시간을 줄여야 한다.

<br/>

## @font-face
```css
@font-face {
  font-family: NanumSquareWeb;
  src: url(NanumSquareR.woff) format('woff');
  font-weight: 400;
}
```
- `font-family` font 속성에서 폰트명으로 지정될 이름을 설정한다.
- `src` 원격 폰트 파일의 위치를 나타내는 URL 값을 지정하거나, 사용자 컴퓨터에 설치된 폰트명을 local 형식으로 지정하는 속성이다.

<br/>

## 웹 폰트 파일 용량 줄이기
### WOFF 2.0 형식 폰트
- WOFF(Web Open Font Format) 형식과 WOFF 2.0 형식(이하 WOFF2 형식)은 **압축된 폰트 형식**이다. WOFF2 형식이 30~50% 더 압축된 형식이다.
### 서브셋 폰트
<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/abb92bf5-8917-47eb-a917-a8a313b31438" width="200px">

- 서브셋 폰트(subset font)는 폰트 파일에서 **불필요한 글자를 제거하고 사용할 글자만 남겨둔 폰트**다.
- 예를 들어 한글의 글자 수는 11,172자 중 사용하지 않는 글자를 제거해서 파일의 용량을 2.4MB -> 586KB로 줄일 수 있었다.

<br/>

## 웹 폰트 렌더링 차단 방식
![images_ken1204_post_14c132af-793b-47f3-8dfb-a71b2e4b4d14_helloworld-201812-webfont_14](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/e34ea93e-3ac4-46a0-9da4-90c8a73d6631)

### FOIT (Flash of Invisible Text)
- 웹폰트 로드가 완료되기 전 까지 텍스트가 안보이는 현상이다.
- 모던 브라우저의 경우 3초 동안 기다리고 그 후에는 시스템 기본 폰트를 보여준다.
### FOUT (Flash of Unstyled Text)
- 브라우저가 웹 폰트를 다운로드하기 전에 텍스트가 대체 글꼴로 렌더링되는 현상이다.
- 폰트에 따라 자간, 높이에 따라 레이아웃이 변경될 수 있다. 이럴 경우 나쁜 사용자 경험을 겪게 된다.

<br/>

## font-display
- CSS의 `font-display` 속성을 사용하면 웹 폰트의 로딩 상태에 따른 동작을 설정할 수 있다.
- `block` FOIT와 동일하게 작동하는 옵션이다. 웹 폰트가 로딩되지 않았을 때는 텍스트를 렌더링하지 않고 (최대 3초), 웹 폰트 로딩이 완료되면 웹 폰트를 적용한다.
- `swap` FOUT와 동일하게 작동하는 옵션이다. 우선 fallback 폰트로 글자를 렌더링하고, 웹 폰트 로딩이 완료되면 웹 폰트를 적용한다. 웹 폰트 로딩 여부와 관계없이 항상 텍스트가 보인다.
- `fallback` 이 옵션을 사용하면 우선 100ms 동안 텍스트가 보이지 않고, 그 후 폴백 폰트로 렌더링한다. 특이한 점은 약 2초의 전환(swap) 시간이 있다는 점이다. 이 시간 안에 로딩이 완료되면 웹 폰트로 전환한다. 하지만 이 시간이 지나면 웹 폰트 다운로드가 완료되어도 웹 폰트로 전환하지 않고 폴백 폰트를 유지한다.
- `optional` fallback 옵션과 비슷하게 우선 100ms 동안 텍스트가 보이지 않고 그 후 폴백 폰트로 전환한다. 이 옵션의 특이한 점은 웹 폰트를 다운로드하더라도 브라우저가 네트워크 상태를 파악해 웹 폰트 전환 여부를 결정한다는 점이다.

<br/>

## preload
```html
<head>
  <link rel="preload" href="../webfont/NanumSquare/NanumSquare.woff" as="font" crossorigin>
</head>
```
- `preload` 옵션은 중요도가 높은 자원(폰트, 이미지, 스크립트 파일 등)을 의도적으로 먼저 로딩할 때 사용하는 것이다.
- 웹 폰트 파일에 `preload` 옵션을 사용하면 CSS 파일보다 먼저 웹 폰트 파일의 다운로드를 시작한다. 



