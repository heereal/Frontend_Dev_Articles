# HTTP Cache
> [Prevent unnecessary network requests with the HTTP Cache](https://web.dev/articles/http-cache?hl=en)   
> [[번역] HTTP 캐시로 불필요한 네트워크 요청 방지](https://web.dev/articles/http-cache?hl=ko)

<br/>

## HTTP 캐시의 작동 방식
- 브라우저가 수행하는 모든 HTTP 요청은 먼저 요청을 처리하는 데 사용할 수 있는 **유효한 캐시된 응답이 있는지 여부를 확인하기 위해 브라우저 캐시로 라우팅**된다.
- 일치하는 응답이 있으면 캐시에서 읽혀지므로 전송으로 인해 발생하는 네트워크 지연 시간과 데이터 비용이 모두 제거된다.

<br/>

## Request headers (기본값 유지)
- 브라우저는 대부분 요청을 보낼 때 개발자를 대신해 헤더를 설정한다.
- `If-None-Match` 및 `If-Modified-Since`와 같이 최신 여부 확인에 영향을 주는 요청 헤더는 브라우저가 HTTP 캐시의 현재 값을 인식하였을 때 표시된다.

<br/>

## Response headers (웹 서버 구성)
- `Cache-Control`: 서버는 Cache-Control 지시어를 반환하여 브라우저 및 기타 중간 캐시가 개별 응답을 **캐시하는 방법과 기간을 지정**할 수 있다.
- `ETag`: 브라우저가 캐시된 응답을 찾으면 작은 **토큰(일반적으로 파일 콘텐츠의 해시)을 서버로 전송하여 파일이 변경되었는지 확인**한다. 서버가 동일한 토큰을 반환하면 파일은 동일한 것이며 다시 다운로드할 필요가 없다.
- `Last-Modified`: 이 헤더는 ETag와 같은 용도로 사용되지만 ETag의 콘텐츠 기반 전략이 아닌 **시간 기반 전략을 사용하여 리소스가 변경되었는지 확인**한다.
- `Cache-Control` 응답 헤더를 생략해도 HTTP 캐싱이 사용 중지되지는 않고 대신 브라우저는 특정 유형의 콘텐츠에 가장 적합한 캐싱 동작 유형을 효과적으로 추측한다.

<br/>

## 버전이 지정된 URL의 장기 캐싱 (versioned URLs)
- **리소스의 URL을 변경**해서 콘텐츠가 변경될 때마다 사용자가 새 응답을 다운로드하도록 한다.
- 일반적으로 파일 이름에 파일의 지문이나 버전 번호를 삽입하는 방식을 사용한다. (예: style.x234dff.css).
- fingerprint 또는 버전 관리 정보가 포함되어 있고 콘텐츠가 변경되지 않아야 하는 URL 요청에 응답할 때는 `Cache-Control: max-age=31536000`을 응답에 추가한다.
- 이 값을 설정하면 향후 1년 동안 동일한 URL을 로드해야 할 때 (31,536,000초, 지원되는 최댓값) 웹 서버에 네트워크 요청을 할 필요 없이 즉시 HTTP 캐시의 값을 사용할 수 있음을 브라우저에 알릴 수 있다.

<br/>

## 버전이 지정되지 않은 URL의 서버 재검증 (unversioned URLs)
- 다음 `Cache-Control` 값을 사용하면 버전이 지정되지 않은 URL이 캐시되는 위치와 방법을 세부적으로 조정할 수 있다.
- `no-cache`: 캐시된 버전의 URL을 사용하기 전에 **매번 서버에서 유효성을 다시 검사해**야 한다고 브라우저에 지시한다. (리소스를 사용할 때마다 서버에서 재검증해야 하는 리소스)
- `no-store`: 브라우저 및 기타 중간 캐시 (예: CDN)에 **어떠한 버전의 파일도 저장하지 않도록 지시**한다. (캐시해서는 안 되는 리소스)
- `private`: 브라우저는 파일을 캐시할 수 있지만 중간 캐시(intermediary caches)는 캐시할 수 없다.
- `public`: 응답은 **모든 캐시에 저장**할 수 있다.

<br/>

<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/c8002891-d75c-46d9-9d0c-0eac076712d2">

- Response header에서 `ETag` 또는 `Last-Modified`를 설정하면 유효성 재검사를 훨씬 더 효율적으로 요청할 수 있다. `ETag`가 더 정확하므로 이 방법을 사용하는 것이 좋다.
- 브라우저가 서버에 `/file`을 요청할 때 `If-None-Match` 헤더를 포함하여 서버에 있는 파일의 `ETag`가 브라우저의 `If-None-Match` 값과 일치하지 않는 경우에만 전체 파일을 반환하도록 서버에 지시한다.
- 이 경우에는 두 값이 일치했으므로 서버는 파일을 캐시해야 하는 기간에 관한 안내와 함께 `304 Not Modified` 응답을 반환한다. (`Cache-Control: max-age=120`)

<br/>

## Cache-Control 플로 차트
![flowchart-8943547beafd6_856](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/ebff3ddd-0d3c-4b45-88d6-b550b43278e7)

