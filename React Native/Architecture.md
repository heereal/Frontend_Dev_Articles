# React Native New Architecture
> [React Native — Ultimate Guide on New Architecture in depth](https://medium.com/@anisurrahmanbup/react-native-new-architecture-in-depth-hermes-jsi-fabric-fabric-renderer-yoga-turbo-module-1284a192a82b)

<br/>

## All components of New Architecture
- **Codegen** (Native code generator)
- **JSI** (JavaScript Interface)
- **Hermes Engine** (A JS engine that runs JS code in devices)
- **Turbo Module** (It Implements Native Module by using JSI & Native Code)
- **Fabric** (Native UI renderer/ New render engine)
- **Fabric renderer** (The new render pipeline creator)
- **Yoga** (Cross platform layout engine)

<br/>

## New Architecture two Phases
### 1. App Build time
- `Codegen`과 `Turno Module`을 켜고 프로덕션 배포 직전에 앱 파일을 생성하기 위해 `build` 명령어를 입력하면 다음의 흐름이 실행된다.
- `JavaScript code`를 `bytecode`로 컴파일한다.
- 빌드 타임 동안 `Codegen`을 사용해서 `native code` 또한 생성된다.
- `bytecode`와 `native code`가 디바이스에 설치할 수 있는 앱 패키지에 포함된다.

### 2. App Run time
- 사용자가 앱을 실행하면 새로운 아키텍처의 나머지 과정들이 실행된다.
- 주로 `Turbo Module`, `Fabric` 두 개의 큰 컴포넌트가 실행된다.

<br/>

## Codegen
- **Generate Native code**: `Codegen`은 `Turbo Module`과 `Fabric` 컴포넌트를 위해 `Native Code`를 생성하는 역할을 한다.
- **Static type checking**: 자바스크립트는 동적 타입 언어이고, C++은 정적 타입 언어이다. `Codegen`은 정적 타입을 체크해서 자바스크립트와 C++ 사이에 타입으로 인한 문제를 해결한다.
- 이렇게 생성된 `native code`는 `typed JavaScript code`와 직접적으로 소통할 수 있다. 

<br/>

## JSI (JavaScript Interface)
- `JSI`는 **C++로 작성**되어서 자바스크립트의 객체와 함수에게 `native interface`를 제공한다.
- C++은 Android, iOS, Windows, macOS 등 다양한 플랫폼에서 실행될 수 있는 언어이기 때문에, 앱을 다른 플랫폼으로 port 하는 데 소요되는 작업량을 줄여준다.
- `JSI`로 인해 네이티브 메서드는 C++ 객체를 통한 자바스크립트에 노출된다. 이 객체들은 자바스크립트 코드를 참조하기 때문에 직접적으로 호출할 수 있다.
- `JSI`는 `Hermes Engine`, `Turbo Module`, `Fabric` 세 개의 컴포넌트에서 사용된다.

<br/>

## Hermes Engine
- `Hermes`는 **앱을 실행할 때 디바이스에서 실행되는 자바스크립트 엔진**이다.
- 앱 사이즈를 줄이고, 메모리 사용량을 향상시키며, 앱 시작 시간을 단축시킨다는 장점이 있다.
- 앱을 실행할 때 `Heremes`는 앱의 `JavaScript code`와 `Native code`를 모두 포함하는 `bytecode`를 로드한다.
- `Hermes`는 `JSI`를 사용해서 앱의 `Native code`와 소통한다. `JSI`는 `Hermes`가 네이티브 함수와 객체에 직접적으로 접근할 수 있도록 한다.
- `Hermes`는 `Fabric`을 이용해서 UI를 업데이트한다.

<br/>

## Turbo Modules
- `Turbo Module`은 `JSI`와 `Native Code`를 사용해서 `Native Module`을 실행한다.
- 사용하지 않는 모듈이라도 모두 초기화했던 이전 `Native Modules`와는 다르게 `Turbo Module`은 앱을 시작할 때 `Native Modules`에 `Lazy Loading`을 적용한다.

<br/>

## Fabric
- `Fabric`은 디바이스에서 UI를 렌더링하는 역할을 한다.
- `Fabric`은 `Hermes`와 `native code`와 소통하기 위해 `JSI`를 이용하기 때문에 네이티브 사이드와 데이터를 주고받을 때 더욱 성능이 좋다.
- 이제 `Fabric renderer`에서 `Suspense`, `Concurrent`와 같은 리액트 18의 기능들을 사용할 수 있다.

<br/>

## Fabric render pipeline

### 1. The Render phase
![image](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/d18ae60c-fd42-4600-8b6c-5eeb6b6dd41a)

- 리액트는 코드를 실행하여 `React element tree`를 생성한다. `React Element`는 순수 자바스크립트 객체로 이루어져 있다.
- `Fabric Renderer`가 `React element tree`를 사용해서 C++로 이루어진 `React shadow tree`를 생성한다.
- 이 과정에서 각 `React element`마다 `shadow node`가 생성된다.

<br/>

### 2. The Commit phase
![image](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/472e3bc1-6cc6-40e6-aba3-862c7f1ad8d4)
- **Layout calculation**: Cross-platform layout engine `Yoga`를 호출해서 각 `React shadow node`의 위치와 크기 등 레이아웃을 계산한다.
- **Tree promotion**: 새로운 `React shadow tree`를 마운트 될 다음 트리로 promote한다. 이 promotion은 `React element tree`의 최신 상태를 나타낸다.

<br/>

### 3. The Mount phase
![image](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/b08328a3-aee4-4df4-bd03-03a0705f782a)

- `layout calculation` 데이터를 포함한 `React Shadow Tree`가 렌더링된 픽셀 값과 함께 `host view tree`(안드로이드 혹은 IOS와 같은 호스트 트리의 view tree)로 변환된다. 
- `Fabric renderer`가 각 `React shadow`에 해당하는 `host view`를 생성하고 이를 화면에 마운트한다.
