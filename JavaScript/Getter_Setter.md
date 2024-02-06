# Getter & Setter
> [자바스크립트 Getter & Setter 완벽 정리](https://inpa.tistory.com/entry/JS-%F0%9F%93%9A-getter-setter-%EB%9E%80)

<br/>

## Getter & Setter 개념
```javascript
const user = {
    name: 'inpa',
    age: 50,
    
    // 객체의 메서드(함수)
    getName() {
    	return user.name;
    },
    setName(value) {
    	user.name = value;
    }
}

console.log(user.getName()); // inpa

user.setName('tistory');
```
- Getter와 Setter는 객체 지향 프로그래밍에서 사용되는 개념으로, 일종의 메서드라고 보면 된다.
- 단어 그대로 `Getter`는 **객체의 속성(property) 값을 반환하는 메서드**이며, `Setter`는 **객체의 속성 값을 설정, 변경하는 메서드**이다.
- 코드 예시와 같이 객체의 프로퍼티에 바로 접근하지 않고 `getName`, `setName` 메서드를 통해 경유해서 접근한다.
- `Getter`와 `Setter`를 사용하면 객체 내부 속성에 직접 접근하지 않아 객체의 정보 은닉을 가능하게 해주어 보안을 강화할 수 있고, 코드의 안전성과 유지보수성을 높일 수 있다는 장점이 있다. 또한 옳지 않은 값을 넣는 것을 사전에 방지할 수 있다. 

<br/>

## 자바스크립트 Getter & Setter
```javascript
const user = {
	name: 'inpa',
    age: 50,
    
    // userName() 메서드 왼쪽에 get, set 키워드만 붙이면 알아서 Getter, Setter 로서 동작된다
    get userName() {
    	return user.name;
    },
    set userName(value) {
    	user.name = value;
    }
}

console.log(user.userName); // inpa

userName = 'tistory';
```
- ES6 최신 자바스크립트부터는 **객체 리터럴 안에서 속성 이름 앞에 `get` 또는 `set` 키워드**를 붙여서 `Getter`와 `Setter`를 간단하게 정의할 수 있게 되었다.
- 이때의 `Getter`와 `Setter`는 함수 호출 형식이 아닌, **일반 프로퍼티처럼 접근해서 사용**한다. `getter`와 `setter` 메서드를 구현하면 객체엔 `userName`이라는 가상의 프로퍼티가 생기는데, 읽고 쓸 순 있지만 실제로는 존재하지 않는 프로퍼티이다.

<br/>

## 접근자 프로퍼티
- 자바스크립트의 객체의 프로퍼티는 데이터 프로퍼티(data property), 접근자 프로퍼티(accessor property) 두 종류로 나눌 수 있다.
- **데이터 프로퍼티**는 객체 내부에 저장된 실제 데이터 값으로서 우리가 일반적인 프로퍼티라고 부르는 대상이다.
- **접근자 프로퍼티**는 일반적인 프로퍼티와 달리 키(key)와 값(value)을 가지지 않고 `getter`와 `setter`라는 함수를 가지는 특수한 프로퍼티이다. 자바스크립트 객체 속성에 접근하듯이 접근자 프로퍼티를 호출하면, 함수 호출 문법이 아니더라도 `getter`와 `setter` 함수가 호출된다.

