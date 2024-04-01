# SEO

## SEO란?
- SEO는 Search Engine Optimization의 줄임말로, **검색 엔진에서 상위권에 노출될 수 있도록 웹 사이트를 최적화하는 작업**을 의미한다.

<br/>

## 세 가지 SEO 전략
<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/c7b7fd5d-d7d2-4bde-beb0-821b5c8ce19c" width="800px">

- **온 페이지(On-Page) SEO**: 웹 사이트의 콘텐츠 구성 요소를 개선
- **테크니컬(Technical) SEO**: 웹 사이트를 검색 엔진이 크롤링하고 색인을 생성하기까지의 과정을 개선
- **오프 페이지(Off-Page) SEO**: 웹 사이트의 외부 평판을 늘리고 개선

<br/>

## sitemap.xml
- 사이트맵은 **웹 사이트의 구조를 검색 엔진에 알려주는 역할을 하는 파일**이다.
- 보통 XML 형식으로 작성되며, 웹 사이트의 모든 페이지의 URL을 포함하고 있다.

<br/>

## robots.txt
- robots.txt는 **현재 웹 사이트에서 크롤링을 허용 또는 허용하지 않을 페이지들을 크롤러에게 알려주는 역할을 하는 텍스트 파일**이다.
- 구글 문서에 따르면 robots.txt는 크롤링으로 인한 과도한 트래픽을 방지하기 위한 목적이지 검색 결과에 노출되지 않기 위한 목적은 아니라고 한다.

<br/>

## 구글 검색 엔진
### Crawler (Googlebot)
- 크롤러는 **소스 코드에서 URL을 추출**하는 기본 파서를 가지고 있다.
- 파서는 페이지를 렌더링하지 않고 소스 코드를 분석하여 `<a href="...">` 스니펫에 있는 모든 URL을 추출한다.
- 크롤러와 인덱서는 서로 긴밀하게 작동하며, 크롤러는 발견한 내용을 인덱서로 보내고, 인덱서는 (예를 들어 JavaScript를 실행하여 발견한) 새 URL을 크롤러에 공급한다.
  
<br/>

### Indexer (Caffeine)
- **웹페이지를 렌더링하고 자바스크립트를 실행**한다.
-  인덱서는 크롤러가 정기적으로 다시 방문하기를 원하는 높은 가치의 URL에 더욱 중점을 두어 크롤러의 URL 우선순위를 지정하는 데 도움을 준다.
  
<br/>

## References
- [JavaScript and SEO: The Difference Between Crawling and Indexing](https://www.stateofdigital.com/javascript-seo-crawling-indexing/)
- [기술 블로그를 위한 SEO](https://wormwlrm.github.io/2023/05/07/SEO-for-Technical-Blog.html)
