# Flexbox
> [An Interactive Guide to Flexbox](https://www.joshwcomeau.com/css/interactive-guide-to-flexbox/)

<br/>

## Flexbox란?
- Flexbox는 구성 요소 그룹을 행이나 열로 정렬하고, 해당 요소의 정렬을 제어할 수 있는 기능을 제공한다.
- 이름에서 알 수 있듯이 Flexbox는 유연성이 핵심이다. 구성 요소의 확장 또는 축소 여부, 여분의 공간 분배 방법 등을 제어할 수 있다.

<br/>

## Flex direction
- 기본적으로 구성 요소는 `row`로 정렬되어 있지만 `flex-direction` 속성을 사용하여 `column`으로 전환할 수 있다.

<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/f84b5226-d711-49f3-8c1b-96ef8d811f2e" width="500px">

- Flexbox의 자식 요소는 기본적으로 다음 두 가지 규칙에 따라 배치되며, `primary axis`를 기준으로 한다.
  - `Primary axis`: 자식 요소는 컨테이너의 시작 부분에 묶여 있다.
  - `Cross axis`: 자식 요소는 컨테이너 전체를 채우기 위해 뻗어나간다.

<br/>

## Alignment
<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/3a735dfb-2651-486f-b3b2-461881ea43a0" width="500px">

- `justify-content` 속성을 사용하여 `primary axis`를 따라 자식 요소가 분배되는 방식을 변경할 수 있다.
- `primary axis`에 관해서는 하나의 자식 요소가 아닌 그룹 분배의 관점에서 생각해야 한다.
- `justify-content`와 `align-items`와 달리, `align-self`는 컨테이너가 아닌 자식 요소에 적용되기 때문에 `cross axis`를 따라 특정 자식 요소의 정렬을 변경할 수 있다.

<br/>

### Content vs. items
- `justify`: `primary axis`를 따라 무언가를 배치한다.
- `align`: `cross axis`를 따라 무언가를 배치한다.
- `content`: 분배할 수 있는 '물건'의 그룹이다.
- `items`: 개별적으로 배치할 수 있는 단일 항목이다.
- `primary axis`를 따라 **그룹의 분배**를 제어하는 `justify-content`와, `cross axis`를 따라 **각 항목을 개별적으로 배치**하는 `align-items`가 있다.

<br/>




