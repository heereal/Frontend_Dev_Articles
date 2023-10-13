# CORS (Cross Origin Resouce Sharing)
> [CORS 에러와 해결법](https://velog.io/@seungchan__y/CORS-%EC%97%90%EB%9F%AC%EC%99%80-%ED%95%B4%EA%B2%B0%EB%B2%95)

<br/>

## Origin이란?
<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/cf2e9b39-a21c-4770-a88b-4ee7b388b992" width="60%">

- Origin은 Protocol, Hostname, Port로 구성되어 있다.

<br/>

## SOP(Same Origin Policy)
- 동일 출처 정책(same-origin policy)은 보안상의 이유로, **다른 Origin으로 부터 요청 받는 리소스 접근을 제한**하는 정책이다.
- 예를 들어, 프론트엔드가 localhost:3000으로 개발 중인 상황에서 백엔드 서버는 localhost:5000에서 호스팅 중인 상황이라면, 이 둘은 서로 포트번호가 달라 다른 Origin으로 취급되어 SOP에 위반된다.

<br/>

## CORS(Cross Origin Resource Sharing)
- **추가 HTTP 헤더를 사용**하여, 한 출처에서 실행 중인 웹 애플리케이션이 다른 출처의 선택한 자원에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제이다.
- 즉, **SOP에 위반 되는 상황 속에서도 리소스에 접근**하려면, CORS 헤더를 도입하여 이러한 상황을 해결해야 한다.

<br/>

## CORS를 도입하는 방법
- **Access-Control-Allow-Origin 응답 헤더 추가**
   ```javascript
   app.use((req, res) => {
    res.header("Access-Control-Allow-Origin", "*"); // 모든 도메인 허용
    res.header("Access-Control-Allow-Origin", "http://localhost:3000"); // 특정 도메인 허용
    });
   ```

   - 응답 헤더의 Access-Control-Allow-Origin 항목을 해당하는 Origin으로 설정해주면 CORS를 도입할 수 있다.
   - 다만 "*"를 이용해 모든 도메인을 허용해 놓는 것은 보안상 좋지 못하니 Origin을 특정해 주는 것이 좋다.
