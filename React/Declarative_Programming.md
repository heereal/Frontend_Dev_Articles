# Declarative Programming
> [Declarative React, and Inversion of Control](https://blog.mathpresso.com/declarative-react-and-inversion-of-control-7b95f3fbddf5)

## 선언형 프로그래밍(Declarative Programming)이란?
```javascript
// 명령형(Imperative) 프로그래밍
List<int> results = new List<int>();
foreach(var num in collection)
{
    if (num % 2 != 0) results.Add(num);
}

// 선언형(Declarative) 프로그래밍
var results = collection.Where( num => num % 2 != 0);
```
> Here, we're saying "Give us everything where it's odd", not "Step through the collection. Check this item, if it's odd, add it to a result collection.”
- 프로그램이 목적지까지 도착하기 위해 어떻게 해야할지를 하나씩 알려주는 것(Imperative)이 아니라, **"내가 원하는 동작"을 명시하는 코드를 작성**하는 것을 의미한다.

<br/>

## 선언형 UI 라이브러리로서의 React
```javascript
// 명령형(Imperative) 프로그래밍
function addCookieToBody() {
  const bodyTag = document.querySelector('body')
  const divTag = document.createElement('div')
  let h1Tag = document.createElement('h1')
  h1Tag.innerText = "Chocolate Cookie"
  divTag.append(h1Tag)
  bodyTag.append(divTag)
}

// 선언형(Declarative) 프로그래밍
function RenderCookie() {
  return (
    <div>
      <h1>Chocolate Cookie</h1>
    </div>
  )
}
```

- `<div>` 태그 안에 `<h1>` 태그가 있고, 그 안에 “Chocolate Cookie”라는 문구가 적힌 HTML 문서를 렌더링하고 싶다고 생각해 보자.
- **명령형(Imperative) 프로그래밍** 방식으로 이 UI를 렌더링하는 경우, DOM을 어떤 순서로 조작할지에 대해 하나씩 순차적으로 알려주어야 할 것이다.
- **선언형(Declarative) 프로그래밍** 방식으로 렌더링하는 경우, 렌더링이 끝난 후에 보기를 원하는 최종 결과물을 “선언”하고, 해당 결과물을 렌더링하는 것은 UI 라이브러리의 책임으로 넘기게 된다.
- 결국 React 개발자는 매 렌더마다 DOM을 어떻게 조작할지에 대해 신경 쓸 필요없이, 특정 상태에 따른 **최종 UI의 결과물을 “선언”해서 React Element의 형태로 React에 전달**하고, **이를 DOM에 반영하는 것은 React의 책임**으로 넘기게 되는 것이다.

<br/>

- DOM에 화면을 렌더할 책임이 개발자에서 React로 넘어오게 되며 이는 DOM을 조작해서 UI를 화면에 그리는 작업에 대한 **제어권이 역전**되었음(Inversion of Control)을 의미한다.
- React가 Component의 Description(React Element들에 대한 정보)을 가지고 DOM을 조작해서 화면을 그리는 책임을 가져가게 된다는 것은 **React가 필요에 의해 렌더링을 위한 여러 작업들의 우선순위를 지정하거나, 작업을 수행하는 것을 미룰 수 있음**을 의미한다.
- 상대적으로 빠르게 반영되어야 하는 User Event(Mouse Click, Keyboard Input)에 의한 렌더링 작업들을 우선적으로 처리하고, Background Data Fetching과 같은 이벤트들에 대해서는 상대적으로 나중에 반영하는 등의 성능 최적화를 React가 자체적으로 수행할 수 있다. (Concurrent React)


