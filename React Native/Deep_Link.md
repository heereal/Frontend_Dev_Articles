# Deep Link
> [Android, iOS 웹뷰에서 딥링크 열기](https://blog.tossbusiness.com/articles/dev-4?utm_source=tossbusiness&utm_medium=blog&utm_campaign=dev-10)   
> [딥링크 실전에서 잘 사용하는 방법](https://blog.tossbusiness.com/articles/dev-10)

<br/>

## 딥링크란?
- 딥링크는 **사용자를 특정 앱으로 이동시키는 기능**이다.
- 예를 들어 사용자가 온라인 쇼핑몰에서 결제 수단으로 토스페이를 선택했을 때 토스 앱의 결제 페이지로 이동한다.

<br/>

## 딥링크의 유형
<img src="https://core-cdn-fe.toss.im/image/optimize/?src=https://static.toss.im/ipd-tcs/toss_core/live/e213ecee-f002-424b-a6b4-560126ae14a9/Untitled.png?&w=1920&q=75">

### 1. URL 스킴
- URL 스킴은 iOS와 Android에서 모두 사용할 수 있는 딥링크 방식으로 문법은 `Scheme://Path`이다.
- `Scheme`은 앱에서 설정할 수 있는 고유한 값이다. `Scheme` 값은 다른 앱에서 중복될 수 있기 때문에 보안에 취약하다는 단점이 있다.
- `Path`는 실행한 앱에서 이동하고 싶은 특정 화면이다. 별도의 `Path`가 없어도 일반적으로 앱을 여는데 문제가 없지만, 앱에서 특정 `Path`가 있어야만 앱이 열리게 구현해놓은 경우도 있다.

<img src="https://core-cdn-fe.toss.im/image/optimize/?src=https://static.toss.im/ipd-tcs/toss_core/live/3013deef-aad0-41df-bea1-921db3723f58/Untitled.png?&w=1920&q=75">

- 예를 들어 원스토어, Google Play 스토어, Galaxy Store 앱은 동일한 `market://` 스킴을 가지고 있기 때문에 **Android** 환경에서 실행할 경우 이미지와 같은 연결 프로그램 화면이 뜬다.
- 하지만 **iOS**에서는 두 개 이상의 앱이 동일한 URL 스킴을 등록한 경우 어떤 앱에 해당 스킴이 부여될지 결정하는 프로세스가 없다. URL 스킴의 이런 취약점 때문에 Apple에서는 공식적으로 Univeral Link를 사용하는 것을 추천한다.

<br/>

### 2. App Link와 Universal Link
- Android 및 iOS에서 각각 제공하는 유사한 방식의 딥링크이다.
- URL 스킴과 달리 App Link, Universal Link는 표준 웹링크 형태이다. `https`로 시작하는 URL을 제공하고, 앱이 설치되지 않은 경우 대체 페이지로 이동시킬 수 있다.
- 예를 들어 서비스가 웹에서 `www.my-service.com`에 운영되고 있다면, 이 링크를 그대로 앱의 딥링크로 사용한다. 사용자의 폰에 앱이 없다면 폰 브라우저에서 웹페이지가 그대로 열린다.
- App Link와 Universal Link는 사용자의 액션으로만 작동하기 때문에 스크립트로 클릭을 유발하면 앱으로 이동하지 않고, 그대로 웹 브라우저에서 링크가 열리는 단점이 있다.

<br/>

### 3. Intent 스킴
```javascript
intent:
   HOST/URI-path // Optional host
   #Intent;
      package=\\[string\\];
      action=\\[string\\];
      category=\\[string\\];
      component=\\[string\\];
      scheme=\\[string\\];
   end;
```
- Android 환경에서 사용할 수 있는 스킴이다.
- Intent 스킴은 위와 같이 앱의 스킴, 패키지 등 많은 정보를 담으며 상당히 복잡한 형태를 가지고 있다.
- 복잡하지만 개발자 입장에서는 Intent 스킴에서 제공하는 정보를 가공해서 다양한 방식으로 앱을 열 수 있다. 예를 들어 앱이 설치되지 않았거나 invalid한 상태인 것을 확인하고 앱 패키지 정보로 플레이 스토어를 열 수 있다.

