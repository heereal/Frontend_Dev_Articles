# SEO

## Crawler (Googlebot)
- 크롤러는 **소스 코드에서 URL을 추출**하는 기본 파서를 가지고 있다.
- 파서는 페이지를 렌더링하지 않고 소스 코드를 분석하여 `<a href="...">` 스니펫에 있는 모든 URL을 추출한다.
- 크롤러와 인덱서는 서로 긴밀하게 작동하며, 크롤러는 발견한 내용을 인덱서로 보내고, 인덱서는 (예를 들어 JavaScript를 실행하여 발견한) 새 URL을 크롤러에 공급한다.
  
<br/>

## Indexer (Caffeine)
- **웹페이지를 렌더링하고 자바스크립트를 실행**한다.
-  인덱서는 크롤러가 정기적으로 다시 방문하기를 원하는 높은 가치의 URL에 더욱 중점을 두어 크롤러의 URL 우선순위를 지정하는 데 도움을 준다.
  
<br/>

## References
- [JavaScript and SEO: The Difference Between Crawling and Indexing](https://www.stateofdigital.com/javascript-seo-crawling-indexing/)
