# robots.txt
## What is a robots.txt file?
- `robots.txt` 파일은 웹사이트의 루트 디렉터리에 있는 텍스트 문서로, 검색 엔진 봇에게 일련의 지침 역할을 한다.
- 검색 엔진이 도메인의 페이지를 처음으로 방문하기 전에 해당 도메인의 `robots.txt` 파일을 연다. 이를 통해 **해당 사이트에서 방문이 허용된 URL과 허용되지 않은 URL을 알 수 있다**.
- CSS 및 JavaScript 파일을 차단하면 구글이 의도한 대로 웹사이트를 렌더링할 수 없기 때문에 `robots.txt` 파일에서 CSS 및 JavaScript 파일은 차단하면 안 된다.

<br/>

## Pros and cons of using robots.txt
### Pro: managing crawl budget
- 일반적으로 검색 스파이더는 얼마나 많은 페이지를 크롤링할지(또는 사이트의 권한/규모/평판 및 서버의 응답 효율성에 따라 소요되는 리소스/시간) '허용량'을 미리 정한 후 웹사이트데 도착하는데, 이를 크롤링 예산이라고 한다.
- 웹사이트 크롤링 예산에 문제가 있다면 검색 엔진이 사이트의 중요하지 않은 부분에 에너지를 '낭비'하지 않도록 차단하여 중요한 섹션에 집중할 수 있다.

### Pro: A note on blocking query parameters
- 사이트에서 목록을 필터링하거나 정렬하기 위해 많은 query parameter를 사용하면 유효한 URL이 많이 생성되며, 모두 크롤링될 수 있다. 
- query parameter가 크롤링되지 않도록 차단하면 검색 엔진이 사이트의 주요 URL만 스파이더링하고 사용자가 만든 거대한 스파이더 함정에 빠지지 않도록 하는 데 도움이 된다.

### Con: not removing a page from search results
- `robots.txt` 파일을 사용하여 크롤러가 사이트에서 어디로 갈 수 없는지 알려줄 수는 있지만, 검색 엔진에게 검색 결과에 표시하지 말아야 할 URL을 알려주는 데 사용할 수는 없다. 즉, 차단한다고 해서 색인화되는 것을 막을 수는 없다.

<br/>

## Robots.txt syntax
```
User-agent: * 
Disallow: / 

User-agent: Googlebot 
Disallow: 

User-agent: bingbot 
Disallow: /not-for-bing/
```

### The user-agent directive
- `robots.txt` 파일의 각 지시문은 `User-agent`로 시작한다.
- `User-agent`는 이 파일이 지정하는 특정 스파이더의 이름이다. `User-agent`에 와일드카드를 사용하여 모든 검색 엔진에 대해 하나의 블록을 사용하거나, 특정 검색 엔진에 대해 특정 블록을 사용할 수 있다.

### The disallow directive
- 지시어 블록의 두 번째 줄에는 `Disallow`가 위치한다. 지정된 스파이더가 액세스할 수 없는 사이트 부분을 지정하는 역할을 한다.
- `Disallow` 줄이 비어 있으면 스파이더가 사이트의 모든 섹션에 액세스할 수 있다는 것을 의미한다.

<br/>

## References
- [The ultimate guide to robots.txt](https://yoast.com/ultimate-guide-robots-txt/)
