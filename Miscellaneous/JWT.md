# JSON Web Token(JWT)
> [[JWT] JSON Web Token 소개 및 구조](https://velopert.com/2389)

<br/>

## JWT란?
- JWT는 웹표준(`RFC 7519`)으로서 JSON 객체를 사용하여 가볍고 자가수용적인(self-contained) 방식으로 정보를 안전성 있게 전달해준다.
- JWT는 C, Java, Python, C++, R, C#, PHP, JavaScript, Ruby, Go, Swift 등 대부분의 주류 프로그래밍 언어에서 지원된다.
- JWT는 토큰에 대한 기본 정보, 전달할 정보, 토큰 검증됐다는 것을 증명하는 signiture 등 필요한 모든 정보를 자체적으로 지니고 있다.
- JWT는 자가수용적이므로 두 개체 사이에 손쉽게 전달 될 수 있다. 웹서버의 경우 HTTP의 헤더에 넣어서 전달할 수도 있고, URL의 파라미터로 전달할 수도 있다.

<br/>

## 회원 인증에서의 JWT 사용
- 사용자가 로그인을 하면 서버는 유저의 정보에 기반한 토큰을 발급하여 유저에게 전달한다.
- 그 후 유저가 서버에 요청을 할 때 마다 JWT를 포함하여 전달한다.
- 서버가 클라이언트에게서 요청을 받을 때마다 해당 토큰이 유효하고 인증됐는지 검증을 하고, 유저가 요청한 작업에 권한이 있는지 확인하여 작업을 처리한다.
- 서버 측에서는 유저의 세션을 유지하지 않기 때문에 세션 관리가 필요 없어서 서버 자원을 아낄 수 있다.

<br/>

## JWT의 구조
![jwt](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/14710ef6-f192-48d1-b4b9-0ec46812e0b8)

JWT는 `.`을 구분자로 3가지의 문자열로 구성되어있다. 

<br/>

## 헤더 (header)
```javascript
{
  "typ": "JWT",
  "alg": "HS256"
}
```
`header`는 두가지의 정보를 지니고 있다.
- `typ`: 토큰의 타입을 지정한다.
- `alg`: 해싱 알고리즘을 지정한다. 해싱 알고리즘으로는 보통 `HMAC SHA256` 혹은 `RSA`가 사용되며, 이 알고리즘은 토큰을 검증 할 때 사용되는 `signature` 부분에서 사용된다.

<br/>

## 내용 (payload)
```javascript
{
    "iss": "velopert.com",
    "exp": "1485270000000",
    "https://velopert.com/jwt_claims/is_admin": true,
    "userId": "11028373727102",
    "username": "velopert"
}
```
- `payload`에는 토큰에 담을 정보가 들어있다.
- `payload`에 담는 정보의 한 ‘조각’ 을 **클레임(claim)** 이라고 부르고, 이는 `name / value`의 한 쌍으로 이뤄져있다.
- 클레임은 등록된(registered) 클레임, 공개(public) 클레임, 비공개(private) 클레임 세 가지로 분류된다.

<br/>

### 1. 등록된 (registered) 클레임
등록된 클레임은 **토큰에 대한 정보**를 담기 위하여 이름이 이미 정해져 있는 클레임이다. 등록된 클레임의 사용은 모두 선택적(optional)이다.
- `iss`: 토큰 발급자 (issuer)
- `sub`: 토큰 제목 (subject)
- `aud`: 토큰 대상자 (audience)
- `exp`: 토큰의 만료시간 (expiraton), 시간은 `NumericDate` 형식으로 되어있어야 하며 (예: 1480849147370) 언제나 현재 시간보다 이후로 설정되어야 한다.
- `nbf`: Not Before 를 의미하며, 토큰의 활성 날짜와 비슷한 개념이다. 여기에도 `NumericDate` 형식으로 날짜를 지정하며, 이 날짜가 지나기 전까지는 토큰이 처리되지 않는다.
- `iat`: 토큰이 발급된 시간 (issued at), 이 값을 사용하여 토큰의 age가 얼마나 되었는지 판단 할 수 있다.
- `jti`: JWT의 고유 식별자로서, 주로 중복적인 처리를 방지하기 위하여 사용된다. 일회용 토큰에 사용하면 유용하다.

<br/>

### 2. 공개 (public) 클레임
```javascript
{
    "https://velopert.com/jwt_claims/is_admin": true
}
```
- 공개 클레임은 충돌이 방지된(collision-resistant) 이름을 가지고 있어야 한다.
- 충돌을 방지하기 위해서 클레임 이름을 `URI` 형식으로 짓는다.

<br/>

### 3. 비공개 (private) 클레임
```javascript
{
    "username": "velopert"
}
```
- 서버와 클라이언트 간에 클레임 이름을 협의해서 사용한다.
- 공개 클레임과는 달리 이름이 중복되면 충돌이 생길 수 있으니 유의해야 한다.

<br/>

## 서명 (signiture)
- 서명 헤더의 인코딩값과, 정보의 인코딩값을 합친 후 주어진 비밀키로 해쉬를 하여 생성한다.
- 이렇게 생성된 JWT를 디버거에 입력하면 복호화된 값을 볼 수 있다.

![Untitled-4](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/bf14198c-f4cd-4008-b320-f44ba59f60c6)
