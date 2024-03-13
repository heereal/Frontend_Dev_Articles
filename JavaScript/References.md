# References in JavaScript

## What is a Reference?
```javascript
let word = "hello"
```
- 변수 자체는 상자가 아니다. 변수 `word`는 `"hello"`가 있는 상자를 가리키고 있다.

```javascript
word = "world"
```
- `"world"`가 담긴 완전히 새로운 상자가 생성되고, `word`가 새 상자를 가리키도록 단어가 재할당된다.
- 그리고 어느 시점에서 `"hello"` 상자는 어디에도 사용하지 않기 때문에 가비지 컬렉터에 의해 정리된다.

<br/>

## Two Types of Types
### Primitive Types
- string, number, boolean, undefined, null과 같은 기본 유형이 있다.
- 이러한 유형은 `read-only`라고도 하며 `immutable`이기 때문에 변경할 수 없다.
- 변수가 이러한 기본 유형 중 하나를 보유하면 값 자체를 수정할 수 없고, **해당 변수를 새 값으로 재할당**할 수만 있다.

### Refrence types
- objects, arrays, functions과 Map, Set과 같은 데이터 구조의 객체 유형이 포함된다.
- 원시 유형과의 가장 큰 차이점은 **객체는 변경 가능**하다는 점이다. 상자의 값을 변경할 수 있는 것이다.

<br/>

## Immutable is Predictable
- 함수에 원시 타입의 값을 전달하면 전달된 원래 변수는 그대로 유지된다. 함수는 그 안에 있는 내용을 수정할 수 없다.
- 하지만 함수에 객체를 전달하면 해당 함수가 객체를 변경할 수 있다. 
- 변수가 예기치 않게 변경되지 않을 것이라는 확신이 있을 때 코드가 무엇을 하는지 파악하기가 더 쉽기 때문에, 많은 사람들이 `immutable` 방식으로 코드를 작성하려고 한다.

<br/>

## Modifying the Contents of the Box
```javascript
let book = {
  title: "Tiny Habits",
  author: "BJ Fogg",
  isCheckedOut: false
}

let backup = book

book.isCheckedOut = true

console.log(backup === book)  // true!
console.log(backup.isCheckedOut)  // also true!!
```
- 변수는 계속해서 동일한 객체를 담고 있는 동일한 상자를 가리키기 때문에 변경된 것은 해당 객체의 속성 중 하나뿐이다. 즉, 객체는 변경되지 않았다.
- 만약 `book`을 수정하기 전에 다른 변수에 저장하여 `backup`을 만들더라도 새로운 객체가 생성되는 것은 아니다.

<br/>

## Mutating an Object in a Function
```javascript
function pureCheckoutBook(book) {
  let copy = { ...book }

  // this change will only affect the copy
  copy.isCheckedOut = true

  // gotta return it, otherwise the change will be lost
  return copy
}

let book = {
  title: "Tiny Habits",
  author: "BJ Fogg",
  isCheckedOut: false
}

// This function returns a new book,
// instead of modifying the existing one,
// so replace `book` with the new checked-out one
book = pureCheckoutBook(book);
```
- `book.isCheckedOut = true`은 함수 내부에서 발생하든 외부에서 발생하든 상관없이 `book` 객체의 내부를 수정할 것이다.
- 이런 일이 발생하지 않도록 하려면 복사본을 만든 다음 복사본을 변경해야 한다.

<br/>

## References
- [A Visual Guide to References in JavaScript](https://daveceddia.com/javascript-references/)
