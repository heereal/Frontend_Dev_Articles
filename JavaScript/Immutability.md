# Immutability
> [Immutability in React and Redux: The Complete Guide](https://daveceddia.com/react-redux-immutability-guide/)

<br/>

## What Is Immutability?
- `immutable`은 `mutable`과 반대되는 개념으로, `mutable`은 변경 및 수정이 가능하다는 뜻이다. 따라서 `immutable`은 변경할 수 없는 것을 의미한다.
- `immutable`하기 위해서는 **기존 변수를 사용하는 대신 새로운 값을 생성해서 기존 값을 대체**해야 한다.
- 예를 들면 자바스크립트의 특정 배열 메서드는 `immutable`하다. 즉, 원본 배열을 수정하는 대신 새로운 배열을 반환한다.

<br/>

## How Referential Equality Works in JavaScript
- `===` 연산자를 사용하여 두 객체 또는 배열을 비교할 때 자바스크립트는 실제로 객체 또는 배열이 가리키는 주소, 즉 **참조를 비교**한다.
- 객체나 배열의 내부를 수정하더라도 객체나 배열의 참조는 변경되지 않는다.

```javascript
// This creates a variable, `crayon`, that points to a box (unnamed),
// which holds the object `{ color: 'red' }`
let crayon = { color: 'red' };

// Changing a property of `crayon` does NOT change the box it points to
crayon.color = 'blue';

// Assigning an object or array to another variable merely points
// that new variable at the old variable's box in memory
let crayon2 = crayon;
console.log(crayon2 === crayon); // true. both point to the same box.

// Niw, any further changes to `crayon2` will also affect `crayon1`
crayon2.color = 'green';
console.log(crayon.color); // changed to green!
console.log(crayon2.color); // also green!
```
- 한 객체를 다른 객체에 할당할 때, 다른 객체는 첫 번째 객체와 동일한 메모리 위치에 대한 또 다른 포인터일 뿐이다. 
- 두 번째 객체에 대한 모든 작업은 첫 번째 객체의 값에도 직접적인 영향을 미친다.
  
<br/>

## A Code Example with Mutation
```javascript
function giveAwesomePowers(person) {
	person.specialPower = "invisibility";
	return person;
}

// Initially, Bob has no powers :(
console.log(person);

// Then we call our function...
let samePerson = giveAwesomePowers(person);

// Now Bob has powers!
console.log(person);
console.log(samePerson);

// He's the same person in every other respect, though.
console.log('Are they the same?', person === samePerson); // true
```
- `giveAwesomePowers`에서 반환된 객체는 함수에 전달된 객체와 동일한 객체이지만 내부의 속성이 변경되었다. 이것을 `mutated`라고 표현한다.
- 객체의 내부 속성이 변경되었지만 객체 참조는 변경되지 않았다. 따라서 `person === samePerson`은 `true`가 된다.
- `push`, `pop`, `shift`, `unshift`, `sort`, `reverse`, `splice` 등 자바스크립트의 특정 배열 메서드는 사용되는 배열을 `mutate`한다.

<br/>

## A Pure Version of giveAwesomePowers
```javascript
function giveAwesomePowers(person) {
  let newPerson = {
    ...person,
    specialPower: 'invisibility'
  }

  return newPerson;
}
```
- `immutable`한 방식으로 배열을 처리하고 싶다면 배열의 복사본을 만든 다음, 복사본을 변경하는 방법이 있다.
