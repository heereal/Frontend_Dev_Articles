# Tree Shaking

## Tree Shaking이란?
- 해당 모듈에서 **실제로 사용하고 있는 코드만 빌드**하기 위해 사용하는 것이 Tree Shaking이다.
- 나무를 흔들어서 죽은 나뭇잎들을 떨어뜨리듯 코드를 빌드할 때도 실제로 쓰지 않는 코드들을 제외한다는 뜻으로 Tree Shaking이란 이름이 붙여졌다.

<br/>

## Tree Shaking 적용 방법
### Babelrc 파일 설정
```javascript
// babel.config.js
export default {
  presets: [
    [
      "@babel/preset-env", {
        modules: false
      }
    ]
  ]
}
```
- Babel은 자바스크립트 문법이 브라우저에서 호환이 가능하도록 `ES5` 문법으로 변환하는 라이브러리이다. 
- Babel은 `import`를 `require()` 구문으로 변환을 시키는데, `require`는 `export` 하는 모든 모듈을 가져오게 된다.
- 따라서 Babel이 `ES6` 문법을 `CommonJS`로 변환하지 않도록 설정을 해야 한다.
- `babel-preset-env`에 `modules`를 `false`로 하면, `import`, `export`의 구문을 `require`, `module.exports` 구문으로 변환시키지 않는다.

<br/>

### 모듈 내 Side-Effect 발생 여부 확인
- 현재 모듈 외에 다른 코드에 영향을 끼치는 요소가 있으면, 이를 Side-Effect가 있다고 표현한다.
```javascript
let animals = ['dog', 'cat'];

const addAnimals = (name) => {
  animals.push(name);
}
```
- 상단의 코드에서 실제로 `addAnimals()` 라는 함수가 쓰이지 않아 다른 코드에 영향을 주지 않는다 해도, `addAnimals()` 함수 바깥의 변수인 `animals`를 변경하는 작업으로 인해 Side-Effect를 일으킨다고 판단하여 Tree Shaking을 하지 못하게 된다.
- 외부 변수의 값을 변경하지 않고, 모듈 내 코드로만 봤을 때 인풋 파라미터 값에 의해 아웃풋 결과값을 예측할 수 있도록 되어 있어야 Side-Effect를 일으키지 않아 Tree-Shaking 하기에 안전한 모듈이라고 할 수 있다.
  
```javascript
{
  "name": "webpack-tree-shaking-example",
  "version": "1.0.0",
  "sideEffects": false
}
```
- `package.json`에서 모든 모듈에 Side-Effect가 발생하지 않는다고 설정할 수 있다.

<br/>

### 필요한 모듈만 Import 해서 가져오기
```
// bad
import * from '../utilFile';

// good
import { module1, module2 } from '../utilFile';
```
- `utilFile` 내에 일부만 `import`를 해서 가져오고 있다.

<br/>

## 만약 Tree Shaking이 되지 않는다면?
- 모든 조건을 맞췄는데도 사용하려는 외부 코드 혹은 라이브러리가 Tree Shaking이 되지 않을 때가 있다.
- 그럴 땐 `import` 해서 불러오려는 코드가 `ES6(export)`로 내보내고 있는지 확인할 필요가 있다.
- 만약 `ES6`가 아니라 `CommonJS (modules.export)`로 내보내고 있다면, 이는 Tress Shaking을 할 수 없는 모듈인 것이다.
- 가장 대표적인 예시로 표준 `lodash` 라이브러리가 있다. 대신 `lodash-es`라는 모듈을 이용하면 Tree Shaking이 가능한 것 같다.

<br/>

## Reference
- [웹 성능 최적화를 위한 Tree Shaking 소개](https://helloinyong.tistory.com/305)
