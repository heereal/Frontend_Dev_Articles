# Blob

## Blob이란?
- Blob(Binary Large Object)은 바이너리 타입의 큰 객체를 나타낸다.
- Blob은 일반적으로 **이미지, 소리, 그리고 멀티미디어 파일**이며 자바스크립트에서 Blob 타입의 객체는 불변성을 지니는 파일과 같은 원시 데이터를 나타낸다.

<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/b8635934-960c-4daa-8ca1-019307d3fd3b" width="500px">

- `Blob` 생성자를 사용해서 `myBlob` 객체를 생성할 경우 `size`와 `type` 2가지 속성을 가진다.

<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/3059cea7-2990-491a-b82a-4046c9595304" width="500px">

- Blob 객체는 `optional type`과 `blobParts`로 이루어져 있다.

<br/>

## Blob API 사용 시나리오
### 1. 청크 업로드
- 용량이 큰 파일을 전송하는 경우 `slice` 메서드를 사용해 파일을 나눈 후 청크로 업로드 할 수 있다.
### 2. 인터넷에서 데이터 다운로드
- `XMLHttpRequest` API를 사용하여 인터넷에서 데이터를 다운로드하고, 이를 Blob 객체에 저장할 수 있다.
### 3. 이미지 압축
- Canvas 객체에서 제공하는 `toDataURL` 메서드를 사용해서 로컬 이미지를 압축한 뒤 서버에 전송할 수 있다.
### 4. Blob URL 생성
- Blob URL/Object URL은 Blob 및 File 객체를 이미지의 URL 소스나 바이너리 데이터를 다운로드하기 위한 링크 등으로 사용할 수 있다.
- `URL.createObjectURL` 메서드를 사용해서 브라우저에서 Blob URL을 생성할 수 있다.
- Blob URL을 생성한 후에는 `URL.revokeObjectURL` 메서드를 호출하여 Blob을 삭제하고, 메모리를 해제할 수 있다.
### 5. Blob에서 Data URL로의 변환
- 오늘날 대부분의 브라우저는 `Data URL`로 불리는 기능을 지원하는데, 이 기능을 통해 이미지와 다른 파일의 바이너리 데이터를 base64로 인코딩하여 웹 페이지에 텍스트 문자열 형태로 나타낼 수 있다.
- 또한 `FileReader` API를 사용하면 간편하게 이미지의 로컬 미리보기 기능을 구현할 수 있다. 

<br/>

## Reference
- [An Introduction to Blob API & Its Use Cases](https://javascript.plainenglish.io/you-dont-know-blob-api-f2c5e9754f29) / [[번역] Blob API에 대한 소개와 활용 사례](https://velog.io/@sehyunny/intro-to-blob-api-and-its-use-cases)
