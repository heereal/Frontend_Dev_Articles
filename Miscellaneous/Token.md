# 토큰 기반 인증
> [[JWT] 토큰(Token) 기반 인증에 대한 소개](https://velopert.com/2350)

<br/>

## 서버 기반 인증 (stateful)
![bb](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/eb4766c4-c152-4f01-a795-a370be960714)

- 클라이언트에서 요청을 받으면 **서버에서 클라이언트의 상태를 유지**한다.
- 메모리, 디스크, DB 등에 사용자들의 정보를 담고 서버가 이를 기억하고 있다.

<br/>

### 서버 기반 인증의 문제점
- **세션**: 사용자의 정보를 서버(세션)에 저장하기 때문에, 만약 로그인 중인 사용자의 수가 많아진다면 서버에 무리를 줄 수 있다.
- **확장성**: 세션을 사용하면 분산된 시스템을 설계하는 것이 어렵기 때문에 서버를 확장하는 것이 어렵다.
- **CORS**: 세션을 관리할 때 자주 사용되는 쿠키는 단일/서브 도메인에서만 작동하도록 설계되어 있기 때문에 쿠키를 여러 도메인에서 관리하는 것이 어렵다.

<br/>

## 토큰 기반 인증 (stateless)
![token-diagram](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/b9e87ebd-dc1d-4cbc-ba49-98d59a4fdc5f)

**상태를 유지하지 않고** 서버는 클라이언트에서 들어오는 요청만으로 작업을 처리한다.
1. 유저가 아이디와 비밀번호로 **로그인**을 한다.
2. 서버 측에서 해당 **계정정보를 검증**한다.
3. 계정 정보가 정확하다면 **서버 측에서** 유저에게 **토큰을 발급**해준다.
4. **클라이언트는 전달 받은 토큰을 저장**해두고, 서버에 요청을 할 때 마다 HTTP 요청의 헤더에 토큰 값을 포함시켜 **토큰을 서버에 함께 전달**한다.
5. 서버는 **토큰을 검증**하고, **요청에 응답**한다.

<br/>

### 토큰 기반 인증의 장점
- **무상태(stateless), 확장성(scalability)**: 토큰을 클라이언트 사이드에 저장하기 때문에 stateless하며, 클라이언트와 서버의 연결고리가 없기 때문에 서버의 확장성(scalability)이 높아진다.
- **보안성**: 클라이언트가 서버에 요청을 보낼 때 더 이상 쿠키를 전달하지 않기 때문에 쿠키를 사용함으로 인해 발생하는 보안의 취약점이 사라진다.
- **확장성(extensibility)**: 토큰을 사용하여 다른 서비스에서도 권한을 공유하는 등 로그인 정보가 사용되는 분야가 확장된다. 예를 들면 웹서비스에서 Google, Facebook 등의 계정으로 로그인을 할 수 있다.
- **여러 플랫폼 및 도메인**: 토큰을 사용하면 CORS가 발생하지 않고 어떤 도메인에서도 토큰만 유효하다면 요청이 정상적으로 처리된다.
- **웹 표준 기반**: 토큰 기반 인증 시스템의 구현체인 JWT는 웹 표준 `RFC 7519`에 등록 되어있다. 따라서 여러 환경에서 지원이 가능하다.
