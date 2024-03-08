# typeof
```javascript
const obj = {
   red: 'apple',
   yellow: 'banana',
   green: 'cucumber',
};

// 위의 객체를 타입으로 변환하여 사용하고 싶을때
type Fruit = typeof obj;
/*
type Fruit = {
    red: string;
    yellow: string;
    green: string;
}
*/

let obj2: Fruit = {
   red: 'pepper',
   yellow: 'orange',
   green: 'pinnut',
};
```
- `typeof`는 **객체 데이터**를 **객체 타입으로 변환**해주는 연산자다.

<br/>

```javascript
function fn(num: number, str: string): string {
   return num.toString();
}

type Fn_Type = typeof fn;
// type Fn_Type = (num: number, str: string) => string

const ff: Fn_Type = (num: number, str: string): string => {
   return str;
};
```
- 함수도 타입으로 변환하여 재사용이 가능하다.

<br/>

# keyof
```javascript
type Type = {
   name: string;
   age: number;
   married: boolean;
}

type Union = keyof Type;
// type Union = name | age | married

const a:Union = 'name';
const b:Union = 'age';
const c:Union = 'married';
```
- `keyof`는 **객체 형태의 타입**을, 따로 속성들만 뽑아 모아 **유니온 타입으로 변환**해주는 연산자다.

<br/>

```javascript
// 상수 타입을 구성하기 위해서는 타입 단언을 해준다.
const obj = { red: 'apple', yellow: 'banana', green: 'cucumber' } as const; 

// 위의 객체에서 red, yellow, green 부분만 꺼내와 타입으로서 사용하고 싶을 때
type Color = keyof typeof obj; // 객체의 key들만 가져와 상수 타입으로
// type Color = "red" | "yellow" | "green"

let ob2: Color = 'red';
let ob3: Color = 'yellow';
let ob4: Color = 'green';
```
- 만일 객체의 키 값을 상수 타입으로 사용하고 싶을 때는 `typeof` 객체 자체에 `keyof` 키워드를 붙여주면 된다.

<br/>

```javascript
const obj = { red: 'apple', yellow: 'banana', green: 'cucumber' } as const;

type Key = typeof obj[keyof typeof obj]; // 객체의 value들만 가져와 상수 타입으로
//  type Key = "apple" | "yellow" | "green"

let ob2: Key = 'apple';
let ob3: Key = 'banana';
let ob4: Key = 'cucumber';
```
- 반대로 객체의 값을 상수 타입으로 사용하고 싶다면 다음과 같이 사용하면 된다.

<br/>

## References
- [객체를 타입으로 변환 - keyof / typeof 사용](https://inpa.tistory.com/entry/TS-%F0%9F%93%98-%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-keyof-typeof-%EC%82%AC%EC%9A%A9%EB%B2%95)
