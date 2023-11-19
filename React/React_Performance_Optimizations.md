# 리액트 최적화

## memo() 사용하지 않고 최적화하기
### Move State Down
```javascript
// as is
export default function App() {
  let [color, setColor] = useState('red');
  return (
    <div>
      <input value={color} onChange={(e) => setColor(e.target.value)} />
      <p style={{ color }}>Hello, world!</p>
      <ExpensiveTree />
    </div>
  );
}
```
- `App` 컴포넌트에서 `color`가 바뀔 때마다 `<ExpensiveTree />` 컴포넌트 또한 리렌더링되고 있다.

<br/>

```javascript
// to be
export default function App() {
  return (
    <>
      <Form />
      <ExpensiveTree />
    </>
  );
}
 
function Form() {
  let [color, setColor] = useState('red');
  return (
    <>
      <input value={color} onChange={(e) => setColor(e.target.value)} />
      <p style={{ color }}>Hello, world!</p>
    </>
  );
}
```
- `Form` 컴포넌트를 생성해서 `color state`를 자식 컴포넌트로 내려주었다.
- 이제 `color`가 바뀌더라도 `Form` 컴포넌트만 리렌더링 될 것이다.

<br/>

### Lift Content Up
```javascript
// as is
export default function App() {
  let [color, setColor] = useState('red');
  return (
    <div style={{ color }}>
      <input value={color} onChange={(e) => setColor(e.target.value)} />
      <p>Hello, world!</p>
      <ExpensiveTree />
    </div>
  );
}
```
- 만약 `color`가 `ExpensiveTree` 컴포넌트에서도 사용되고 있다면 어떻게 해야 될까?

<br/>

```javascript
// to be
export default function App() {
  return (
    <ColorPicker>
      <p>Hello, world!</p>
      <ExpensiveTree />
    </ColorPicker>
  );
}
 
function ColorPicker({ children }) {
  let [color, setColor] = useState("red");
  return (
    <div style={{ color }}>
      <input value={color} onChange={(e) => setColor(e.target.value)} />
      {children}
    </div>
  );
}
```
- `color state`를 생성하며 이에 의존하는 부분은 `ColorPicker` 컴포넌트로 이동했다.
- `color`와 상관없는 `ExpensiveTree` 컴포넌트는 `App` 컴포넌트에 남아서 `ColorPicker` 컴포넌트의 `children props`가 되었다.
- `color`가 변하면 `ColorPicker` 컴포넌트가 리렌더링된다. 하지만 여전히 동일한 `chidren props`를 가지고 있기 때문에 `ExpensiveTree` 컴포넌트는 리렌더링되지 않는다.

<br/>

## Reference
- [Before You memo()](https://overreacted.io/before-you-memo/)
