# Prototype
## 프로토타입이란?
- 자바스크립트는 다른 상속 기반의 언어와 달리 프로토타입 기반의 언어로, **모든 객체는 특정 객체를 원형(prototype)으로 삼고 이를 복제(참조)** 하는 방식을 통해 상속과 비슷한 효과를 가진다.

<br/>

## 프로토타입 개념 추상화 
<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/40dbf287-245d-4fe8-a2f9-f069d304e793" width='300px'>

- 생성자(`Constructor`)는 원형(`prototype`)을 속성으로 가진다.
- 생성자와 `new` 키워드를 결합하면 인스턴스(`instance`)가 생성된다.
- 이때 인스턴스는 자동으로 `__proto__` 속성을 가진다.
- 이 `__proto__` 속성은 생성자의 `prototype`을 참조한다.

<br/>

## 인스턴스와 proto의 관계
```javascript
let Person = function (name) {
	this._name = name;
}
    
Person.prototype.getName = function () {
    console.log('call getName method');
    return this._name;
}

const j113 = new Person("seungchan");
    
j113.__proto__.getName(); 
// call getName method
// undefined

Person.prototype === j113.__proto__ // true
```
- 생성자 함수 `Person`을 정의하고 생성자 함수의 `prototype`에 `getName`이라는 메소드를 정의하였다.
- `j113`이라는 인스턴스를 생성해서 이 인스턴스의 `prototype`에 정의된 `getName`이라는 메소드를 호출하였다.
- 인스턴스가 `prototype`에 정의된 `getName` 메소드에는 잘 도달하지만 `getName`에서 반환하는 `this._name`은 `undefined`가 된다.
- `getName` 메소드를 호출하는 주체가 `j113.__proto__`이고, 이는 곧 `Person`의 `prototype`인데 여기에는 `_name` 이라는 것이 존재하지 않는다. 따라서 위의 예시에서 `undefined`가 나오게 된 것이다.

```javascript
// Person 생성자함수 정의는 생략
Person.prototype._name = "seungchan"
    
const j113 = new Person("seungchan");
    
j113.__proto__.getName(); // seungchan
```
- `Person`의 `prototype` 자체에 `_name` 프로퍼티를 정의해 놓으면 `getName`이 원하는 대로 출력되는 것을 확인할 수 있다.

```javascript
const j113 = new Person("seungchan");
    
j113.getName();// seungchan
```
- 또한, 인스턴스에서 `__proto__`라는 키워드를 생략하더라도 `prototype`에 정의된 메소드 및 프로퍼티에 자유롭게 접근이 가능하다.
  
<br/>

## 메소드 오버라이드
```javascript
let Person = function(name){
	this.name = name;
}

Person.prototype.getName = function() {
	return this.name;
}

const seungchan = new Person('승찬');

seungchan.getName = function () {
	return 'i am ' + this.name;
}

console.log(seungchan.getName()); // i am 승찬
```
- `prototype`에 정의된 메소드와 동일한 이름의 메소드를 인스턴스에 정의하게 될 경우에는 인스턴스의 함수로 덮어씌워진다.

<br/>

## 프로토타입 체이닝
<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/b8820789-245a-4739-8c18-1f0ca2f22735" width="500px">

```javascript
const arr = [1, 2];

arr(.__proto__).push(3); // Array에 정의된 push 메소드
arr(.__proto__)(.__proto__).hasOwnProperty(2); // Object에 정의된 메소드
```
- `[1,2]`의 `__proto__`는 `Array`를 가리키고, 다시 `Array`의 `__proto__`는 `Object`를 가리킨다.
- 이러한 관계 덕분에 `Array`의 인스턴스인 `[1,2]`는 `Array`의 메소드 뿐만 아니라 `Object`에서 정의된 메소드가 까지 사용할 수 있다.
- 모든 데이터 타입은 `prototype`을 가지고 `prototype`은 `Object` 형태를 가지기 때문에 `prototype` 체인의 최상단에는 `Object`가 존재한다.
- 따라서 모든 데이터 타입에서 `Object` 프로토타입에 정의된 메소드들에 접근할 수 있게 된다. `hasOwnProperty`가 대표적인 예이다.
- 하지만 `Object`의 모든 메소드가 모든 데이터 타입에서 사용될 수 있게 설계되어 있지는 않다. 그러한 메소드들은 `Obejcts.keys(...)`와 같이 `Object` 키워드와 함께 사용한다.

<br/>

## instanceof 연산자
```javascript
function Person(name) {
  this.name = name;
}

const me = new Person('Lee');
console.log(me instanceof Person); // true
console.log(me instanceof Object); // true
```
- 좌변에 `객체`를 가리키는 식별자, 우변에 `생성자 함수`를 가리키는 식별자를 피연산자로 받는 이항 연산자다.
- `instanceof` 연산자는 생성자 함수의 `prototype`에 바인딩된 객체가 프로토타입 체인 상에 존재하는지 확인한다.

<br/>

## References
- [Prototype에 대해 이해하기](https://velog.io/@seungchan__y/Prototype%EC%97%90-%EB%8C%80%ED%95%B4-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0)
- [Javascript - instanceof 연산자와 프로토타입 체인](https://velog.io/@dev-redo/Javascript-instanceof-%EC%97%B0%EC%82%B0%EC%9E%90%EC%99%80-%ED%94%84%EB%A1%9C%ED%86%A0%ED%83%80%EC%9E%85-%EC%B2%B4%EC%9D%B8)
