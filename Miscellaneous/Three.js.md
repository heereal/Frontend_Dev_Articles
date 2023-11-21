# Three.js
> [Three.js와의 설레는 첫만남](https://velog.io/@greencloud/Three.js%EC%99%80%EC%9D%98-%EC%84%A4%EB%A0%88%EB%8A%94-%EC%B2%AB%EB%A7%8C%EB%82%A8-)

<br/>

## Three.js란?
- Three.js는 웹페이지에 3D 객체를 쉽게 렌더링하도록 도와주는 **자바스크립트 3D 라이브러리**이다.
- Three.js는 점, 선, 삼각형만을 그리는 단순한 시스템인 `WebGL`을 사용하여 3D 요소를 더욱 간단하게 구현할 수 있다.

<br/>

## Three.js의 구조
<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/81bf2cf3-3b79-4cdc-82ff-9d5ad8fbb9a3">

### Renderer
- Three.js의 핵심 객체이다.
- `Scene`과 `Camera` 객체를 넘겨받아 카메라의 `Frustrum` 안 3D Scene의 일부를 평면 이미지로 렌더링한다.
- Three.js에서 `Frustrum`은 카메라 시야 안에 들어갈 내용물을 결정하는 데 쓰인다. 쉽게 말하면 카메라 렌즈를 통해 보이는 특정 공간을 의미한다.

### Scene Graph
- `Scene` 혹은 다수의 `Mesh`, `Light`, `Group`, `Object3D`, `Camera`로 이루어진 트리 구조와 유사하다.
- `Scene`은 `Scene Graph`의 최상위 노드이다. background color, fog 등의 요소를 포함한다.
- `Scene`에 포함된 객체들도 부모 / 자식의 트리 구조로 이루어져있다.

### Mesh
- `Material`로 하나의 `Geometry`를 그리는 객체이다. 쉽게 이야기하면 **하나의 덩어리**이다.
- 여러 개의 `Mesh`가 하나의 `Material` 혹은 `Geometry`를 동시에 참조할 수 있다.

### Geometry
- `Gemoetry` **객체의 정점 (vertex, 꼭짓점) 데이터**이다.
- 구, 정육면체, 면, 개, 고양이 등 다양한 모양이 될 수 있다.

### Material
- `Geometry` 객체를 그리는 데 사용하는 표면 (Texture) 속성이다.
- 색, 밝기, 텍스처, 반질거림, 투명도 등을 설정할 수 있다.
- 하나의 `Material`은 여러 개의 `Texture`를 사용할 수 있다.

<br/>

## Scene 만들기
### 1. Scene, Camera 생성하기
```javascript
import * as THREE from "three";
      
// Scene 생성
const scene = new THREE.Scene(); 

// Camera 생성
const camera = new THREE.PerspectiveCamera(
  75, // field of view
  window.innerWidth / window.innerHeight, // aspect ratio
  0.1, // near
  1000 // far
); 
```
- Three.js에는 여러 종류의 카메라가 있는데 여기서는 `PerspectiveCamera`를 사용했다.
- 첫 번째 속성은 `field of view` (FOV, 시야각)이다. `FOV`는 해당 시점의 화면이 보여지는 정도를 나타내며, 각도 값으로 설정한다.
- 두 번째 속성은 `aspect ratio` (종횡비)이다. 대부분의 경우는 요소의 높이와 너비에 맞추어 표시한다. 이렇게 하지 않으면 이미지가 틀어져보일 수 있다.
- 세 번째 속성과 네 번째 속성은 `near`과 `far`이다. `far` 값보다 멀리 있는 요소나 `near` 값보다 가까이 있는 오브젝트는 렌더링되지 않는다.

<br/>

### 2. Renderer 생성하기
```javascript
import * as THREE from "three";
      
const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 0.1, 1000 );

// Renderer 생성
const renderer = new THREE.WebGLRenderer(); 

// 렌더링할 곳 크기 설정
renderer.setSize( window.innerWidth, window.innerHeight );

// Renderer 요소를 추가
// renderer.domElement는 <canvas> 요소로, Renderer가 Scene을 나타내는 구역
document.body.appendChild( renderer.domElement );
```
- `Renderer` 인스턴스 생성과 동시에 렌더링할 곳의 크기를 정해줘야 한다. 여기서는 렌더링할 구역의 높이와 너비를 브라우저 윈도우의 크기와 같게 설정했다.
- 사이즈는 그대로 유지하되 더 낮은 해상도로 렌더링하고 싶다면, `setSize`의 세 번째 인자인 `updateStyle`을 `false`로 설정할 수 있다.

<br/>

### 3. Geometry, Material 생성하기
```javascript
 import * as THREE from "three";
      
const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 0.1, 1000 );

const renderer = new THREE.WebGLRenderer(); 
renderer.setSize( window.innerWidth, window.innerHeight );
document.body.appendChild( renderer.domElement );

// Geometry 생성
const geometry = new THREE.BoxGeometry( 
  1, // 가로
  1, // 세로
  1 // 높이
);

// Material 생성
const material = new THREE.MeshBasicMaterial( { color: 0x00ff00 } );

// 큐브 만들고 Scene에 추가
const cube = new THREE.Mesh( geometry, material );
scene.add( cube );

// Camera 위치 수정
camera.position.z = 5;
```
- `BoxGeometry`에는 큐브에 필요한 모든 꼭짓점(vertices)와 면(faces)이 포함되어 있다.
- `new THREE.BoxGeometry( 1, 1, 1 );` 코드를 통해 가로, 세로, 높이가 모두 1인 정육면체 `Geometry`를 만든 것이다. 여기서 1은 1px이나 1cm같은 것이 아니라, 3D 공간에서의 상대적인 크기를 나타낸다.
- `new THREE.MeshBasicMaterial( { color: 0x00ff00 } );` 를 통해 표면의 색상이 `0x00ff00`인 `Material`을 생성한다.
- `Mesh` 객체 생성을 위해서는 `Geometry`와 `Material` 두 가지 요소가 필요하다.
- `scene.add();` 를 호출하면 `scene`에 추가된 모든 것들은 `(0, 0, 0)` 속성을 가진다. 이 경우 카메라와 큐브가 동일한 위치에 있게 되므로, 여기서는 카메라의 위치를 수정했다.

<br/>

### 4. Scene 렌더링
```javascript
import * as THREE from "three";
      
const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 0.1, 1000 );

const renderer = new THREE.WebGLRenderer(); 
renderer.setSize( window.innerWidth, window.innerHeight );
document.body.appendChild( renderer.domElement );

const geometry = new THREE.BoxGeometry( 1, 1, 1 );
const material = new THREE.MeshBasicMaterial( { color: 0x00ff00 } );
const cube = new THREE.Mesh( geometry, material );
scene.add( cube );

camera.position.z = 5;

// 화면이 새로고침될 때마다 렌더링
function animate() {
  requestAnimationFrame( animate );

  // 큐브 회전시키기
  cube.rotation.x += 0.01;
  cube.rotation.y += 0.01;

  renderer.render( scene, camera );
}

animate();
```
- `render loop` 또는 `animate loop`라고 불리는 기능을 추가해서 화면이 새로고침될 때마다 계속 렌더링되도록 했다.
- `setInterval`을 쓰지 않고 `requestAnimationFrame`을 사용하는 데에는 여러 이유가 있지만, 가장 큰 장점은 유저가 브라우저 창에서 이탈했을 때 렌더링을 멈춰준다는 것이다.
- 추가적으로 매 프레임마다 (일반적으로는 1초에 60번 가량) 실행되면서 큐브가 회전하도록 설정했다.

<br/>

### 결과물
![image](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/8624b0d3-aa98-4b86-9a4b-1f946c0b8239)

