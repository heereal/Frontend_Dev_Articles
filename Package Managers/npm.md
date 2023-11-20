# npm

## npm이란?
- NPM은 Node Package Manager의 줄임말로, Node.js의 기본 패키지 관리자이다.
- npm은 기본적으로 다음과 같은 기능을 제공한다.
  - 라이브러리 설치 및 관리
  - 라이브러리의 의존성(dependency) 관리
  - 라이브러리의 업데이트 및 삭제
  - 라이브러리의 버전 확인
  - 라이브러리의 배포
- **의존성**은 한 모듈에서 다른 모듈의 기능을 사용할 때의 관계를 의미한다. 예를 들어 A모듈에서 B모듈의 기능을 사용한다면 A는 B에 종속되어있다, 의존적이다 라고 표현한다. 이 의존성은 낮을수록 좋다.
- `npm init` 혹은 `npm install [모듈 이름]`을 하면 `package.json`, `package-lock.json`, `node_modules` 폴더가 생성된다.

<br/>

## package.json
```
{
  "name": "my-project",
  "version": "1.0.0",
  "description": "My first Node.js project",
  "dependencies": {
    "express": "^4.17.1"
  },
  "scripts": {
    "start": "node server.js",
    "test": "jest"
  },
  "license": "MIT"
}
```
`package.json`은 프로젝트의 이름, 버전, 설명, 종속된 라이브러리 등의 정보를 담은 파일이다. 이 파일을 통하여 협업에서 프로젝트의 정보를 일관되게 공유할 수 있다.
- `name`: 프로젝트의 이름
- `version`: 프로젝트의 버전
- `description`: 프로젝트의 간략한 설명
- `dependencies`: 프로젝트를 실행하기 위해 필요한 라이브러리 목록
- `scripts`: 프로젝트를 실행하거나 테스트하는데 사용되는 명령어
- `license`: 프로젝트를 사용하는데 적용되는 라이선스

<br/>

## package-lock.json
- `npm install`을 실행하면 `package.json`에 명시되어 있는 버전으로 설치 된다. 정확히는 명시되어 있는 버전 위로, 메이저 버전 아래로 설치가 된다.
```
"dependencies": {
  "express": "^4.17.1"
},
```
- 만약 다음과 같은 의존 라이브러리가 적혀 있다면 이는 express 라이브러리를 설치하는데, 4.17.1 버전 위로, 5.0.0 버전 아래로 설치하라는 뜻이다.
- 즉, `npm install` 시점에 express 라이브러리의 버전이 4.20.0으로 업데이트 됐다면, 그 버전을 설치하게 된다. 이는 `package.json` 파일을 사용해도 설치 시점에 따라 서로 다른 버전이 설치될 수 있다는 말이다.
- `package-lock.json`는 설치 시점에 상관없이 명시되어 있는 버전으로만 설치할 수 있게 해주기 때문에 협업을 할 경우 이 `package-lock.json`까지 공유를 해야 모두가 같은 버전의 라이브러리를 사용하여 오류를 방지할 수 있다.

<br/>

## node_modules
- `npm install` 후 생기는 이 폴더는 라이브러리와 그 라이브러리가 의존성으로 가지는 라이브러리를 저장하는 폴더다. 그래서 많은 라이브러리를 설치하게 될 경우 점점 커지게 된다.
- 사용자는 `npm install`을 통해 언제든 이 폴더를 다시 생성할 수 있으므로 공유할 필요가 없다. 따라서 이 폴더는 깃허브 등에 올릴 때 공유하지 않아도 된다.

<br/>

## npm 명령어 목록
- `npm init`: 프로젝트를 생성
- `npm init -y`: 기본적인 package.json 파일을 생성
- `npm install -g`: 전역으로 라이브러리를 설치
- `npm uninstsall -g`: 전역으로 라이브러리를 제거
- `npm list -g`: 설치된 전역 라이브러리를 확인
- `npm publish`: 라이브러리를 npm registry에 배포
- `npm run [script-name]`: 지정된 스크립트를 실행
- `npm run list`: 프로젝트의 스크립트를 확인
- `npm help`: 명령어에 대한 도움말을 표시

<br/>

## npx와의 차이점
```
npx create-react-app my-app
```
- `npx`는 `npm` 버전 5.2부터 같이 설치되어 있는 명령어이다. `npm`이 패키지를 설치하고 삭제하는 관리로서의 명령어 라면 `npx`는 **패키지를 실행하는 데 사용되는 명령어**다.
- 모듈을 로컬에 저장하지 않고, 매번 최신 버전의 파일만을 임시로 불러와 실행 시킨 후에, 다시 그 파일은 없어지는 방식으로 작동한다.
- 예를 들어 `npx`를 통해 `create-react-app`을 설치할 경우 매번 최신 버전만을 가져와서 설치해 주기 때문에 지금 어떤 버전을 사용하고 있는지 신경쓸 필요가 없어진다.

<br/>

## Reference
- [npm과 npx 그리고 yarn](https://velog.io/@sanghyeon/npm%EA%B3%BC-npx-%EA%B7%B8%EB%A6%AC%EA%B3%A0-yarn)
- [npm과 npx의 차이에 대해서](https://ljh86029926.gitbook.io/coding-apple-react/undefined/npm-npx)
