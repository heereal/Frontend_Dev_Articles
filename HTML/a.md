# a 태그
## a 태그란?
```html
<a href=https://seo.tbwakorea.com>TBWA DataLab 블로그</a>
```
- `<a>` 태그는 한 페이지에서 다른 페이지로 연결하는 하이퍼링크를 위해 사용한다.
- `<a>` 태그가 같은 웹사이트 내로 이동하도록 작성되어 있다면, 이를 내부 링크라고 부른다. 반면, `<a>` 태그가 다른 웹사이트로 이동하도록 작성되어 있다면, 이를 외부 링크라고 부른다.

<br/>

## a 태그의 구성 요소와 속성
<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/ea7d5cd4-ddfb-4f99-b317-d045a99a638b" width="700px">

- **오프닝 태그(Opening Tag)**: `<a>` 태그의 시작을 나타냄.
- **태그 속성(Attribute)** 과 **속성값(Attribute value)**: 태그가 링크되는 페이지를 나타내고, 태그를 클릭할 때 태그가 작동하는 방식에 영향을 미침.
- **앵커 텍스트(Anchor Text)**: 사용자가 링크를 방문하기 위해 클릭하는 텍스트. 검색 엔진이나 크롤링 봇은 앵커 텍스트에 기재된 내용이 페이지의 내용과 같다고 이해하기 때문에 이동하고자 하는 다른 페이지의 핵심 키워드를 포함해야 함.
- **클로징 태그(Closing Tag)**: `<a>` 태그의 마지막을 나타내며, `</a>`로 표기함.

<br/>

## a 태그 속성
### 1. href
- `href` 속성은 링크된 페이지의 URL을 명시하고 가리킨다.
- 다른 `<a>` 태그 속성과는 달리, `href` 속성은 필수적으로 사용해야 한다.

 ### 2. hreflang
- `hreflang` 속성은 링크된 페이지가 무슨 언어로 되어 있는지를 명시한다.
- 이 속성은 반드시 `href` 속성이 설정되어야만 사용할 수 있고 `<a hreflang=”언어 코드”>` 형태로 작성한다.
- 언어 코드는 알파벳 두 글자로 이루어져 있으며, ko(한국어), en(영어), zh(중국어), ja(일본어) 등이 있다.

### 3. rel
- `rel` 속성은 현재 페이지와 링크된 페이지 사이의 연관 관계를 명시한다.
- 링크에 대한 더 많은 정보를 검색 엔진에 제공하기 위해 이 속성을 사용하고, `href` 속성이 설정되어 있어야만 사용할 수 있다.

---

- `nofollow`: 유료 링크와 같이 검색 엔진이나 봇이 추적해서는 안 될 때 사용함
- `noreferrer`: 링크된 페이지가 현재 페이지를 방문자 출처로 인식하는 것을 막을 때 사용함
- `noopener`: 사용자가 링크를 클릭할 때 액세스 권한 없이 새 탭에서 링크가 열리도록 할 때 사용함
- `author`: 해당 문서의 저자에 대한 링크를 나타낼 때 사용함
- `external`: 링크된 문서가 현재 문서와 같은 사이트 내에 있지 않음을 나타낼 때 사용함
- `help`: 도움말 문서에 대한 링크를 나타낼 때 사용함

### 4. target
- `target` 속성은 링크된 페이지를 클릭했을 때 페이지가 열릴 위치를 명시한다.
- 만약, `<a>` 태그가 `target` 속성을 포함하고 있지 않다면, 이는 디폴트로 `“_self”`를 `target` 속성값으로 가지게 된다.

---

- `_blank`: 링크된 페이지를 새로운 윈도우나 탭에서 오픈함
- `_self`: 링크된 페이지를 현재 위치한 페이지에서 오픈함 (기본값)

### 5. type
- `type` 속성은 링크된 페이지의 인터넷 미디어 타입(MIME 타입)을 명시한다. 이 속성은 반드시 `href` 속성이 설정되어야만 사용할 수 있다.
- `type` 속성은 `<a type=”application/javascript”>`와 같이 최상위 유형/하위 유형 형식으로 작성한다.

### 6. download
- `download` 속성은 링크를 클릭할 때 대상 페이지로 연결되지 않고 해당 콘텐츠가 다운로드됨을 명시한다.
- 작성 형태는 `<a download=”파일 이름”>`으로, 속성값에는 다운로드되는 파일의 이름이 들어가야 한다. 만약 속성값을 생략한다면, 디폴트로 파일의 원래 이름이 사용된다.

<br/>

## References
- [a 태그란 무엇인가? – 구성 요소와 속성, SEO에 미치는 영향](https://seo.tbwakorea.com/blog/what-is-a-tag/?utm_source=oneoneone)