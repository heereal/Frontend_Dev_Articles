## @next/font
> [How @next/font works / Zero Layout Shift를 위한 Next Font Optimization의 원리](https://blog.mathpresso.com/how-next-font-works-8bb72c2bae39)

<br/>

### @next/font의 기능
- 사용자에게 네트워크 환경과 상관없이 최대한 일관적인 UX 경험을 제공하는데 초점을 맞추고 있다.
1. adjustFallbackFont 등의 기능을 이용한 zero layout shift 지원
2. 빠른 font loading

<br/>

### zero layout shift
<img src="https://miro.medium.com/v2/resize:fit:640/0*nYvksJpChrkld9k7.gif">

- `adjustFallbackFont` 기능을 통해 기존 Fallback Font의 size-adjust 속성을 조정하여 **Fallback 폰트와 google font 사이의 크기 차이가 발생하지 않는다**.

<br/>

### pre-download google font
-  build 타임에 미리 google font를 다운로드하여서 **로컬 디렉터리에 저장**해 두고, html 파일이 이 로컬 파일을 link 하도록 구현된다.
-  이렇게 하면 서로 다른 도메인 간 Connection 연결을 위한 handshaking 과정 없이, 이미 HTML 파일을 다운로드하기 위해 생성했던 Connection을 그대로 사용할 수 있기 때문에 전자보다 비교적 빠른 속도로 파일을 다운로드할 수 있다.
-  fallback font의 size-adjust를 수행 -> @font-face에서 폰트 파일을 다운로드 -> 다운로드한 폰트와 생성한 css 파일을 className과 css에 바인딩
