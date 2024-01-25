# 메모리 할당
> [JavaScript's Memory Management Explained](https://felixgerschau.com/javascript-memory-management/)

<br/>

## Memory life cycle
<img width="600" alt="memory-life-cycle" src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/0f0930e1-9d8b-41c7-b313-a6dfb2e4f314">

### Allocate memory (메모리 할당)
- 변수, 함수 등을 생성할 때 자바스크립트 엔진이 이를 위한 메모리를 할당한다.

### Use memory (메모리 사용)
- 메모리 사용은 코드에서 명시적으로 수행하는 작업이다.

### Release memory (메모리 해제)
- 할당된 메모리가 해제되면 다른 용도로 사용할 수 있는 공간이 확보된다.

<br/>

## The memory heap and stack
<img width="600" alt="stack-heap-pointers" src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/1b9f9ad2-d116-4f3c-b005-a60826745c75">

- 자바스크립트 엔진은 메모리 힙과 스택, 두 곳에 데이터를 저장한다.

<br/>

### Stack: Static memory allocation
- 스택은 자바스크립트가 **정적 데이터를 저장**하는 데 사용하는 데이터 구조다.
- 정적 데이터는 엔진이 **컴파일 시점에 크기를 알고 있는 데이터**이다.
- **원시 값(strings, numbers, booleans, undefined, null)** 과 **객체 및 함수를 가리키는 참조**가 스택에 저장된다.
- 엔진은 크기가 변하지 않는다는 것을 알고 있기 때문에 각 값에 대해 **고정된 양의 메모리를 할당**한다.

<br/>

### Heap: Dynamic memory allocation
- 힙은 자바스크립트가 **객체와 함수를 저장**하는 공간이다.
- 엔진은 스택과 달리 **객체에 제한을 두지 않고 메모리를 할당**한다. 대신 필요에 따라 더 많은 공간이 할당된다.
- 이러한 방식으로 메모리를 할당하는 것을 **동적 메모리 할당**이라고 한다.

```javascript
const person = {
  name: 'John',
  age: 24,
};
```
- 자바스크립트는 힙에 `person` 객체에 대한 메모리를 할당한다. 반면에 실제 값은 여전히 원시 타입이기 때문에 스택에 저장된다.
- 힙에 새 객체가 생성되고, 스택에 해당 객체에 대한 참조가 생성되는 것이다.
