# Flexbox
> [An Interactive Guide to Flexbox](https://www.joshwcomeau.com/css/interactive-guide-to-flexbox/)

<br/>

## Flexbox
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

## flex-basis
- Flex `row`에서 `flex-basis`는 `width`와 같은 역할을 한다. Flex `column`에서 `flex-basis`는 `height`와 같은 역할을 한다. 
- `flex-basis`는 `width`나 `height`와 비슷하지만 `primary axis`에 고정되어 있다. 
-  `width`나 `height`와 다른 점은 `primary axis`가 수평이든 수직이든 상관없이 똑같은 방식으로 작동한다는 것이다.

<br/>

## flex-grow
- `flex-grow`는 **항목이 컨테이너보다 작을 때 여분의 공간을 분배**하는 방법을 제어한다.
- `flex-grow`의 기본값은 `0`이며, 이 경우에 여분의 공간은 분배되지 않는다. 자식 요소가 컨테이너의 여분의 공간을 차지하도록 하려면 `flex-grow`를 명시적으로 설정해야 한다.
- 여러 자식 요소에 `flex-grow`를 설정한 경우, 여분의 공간은 `flex-grow`의 값에 따라 **비례적으로** 자식 요소들에게 나누어진다.

<br/>

## flex-shrink
- `flex-shrink`는 **항목이 컨테이너보다 클 때 공간을 제거**하는 방법을 제어한다.
- `flex-shrink` 속성은 절대값이 아닌 **비율로 처리**된다.

<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/66ba86c0-12db-47ee-8688-bee803c38faa" width="500px">
  
- 부족한 공간이 총 `100px`이라면 일반적으로 두 개의 자식 요소가 각각 1/2을 지불한다.
- 하지만 `flex-shrink`를 사용하면 첫 번째 요소는 3/4(75px)을 지불하고 두 번째 요소는 1/4(25px)을 지불하게 된다.

<br/>

### Preventing shrinking
- Flex의 자식 요소가 줄어드는 것을 원치 않는다면 `flex-shrink: 0`으로 설정하면 된다.
- `flex-shrink`를 `0`으로 설정하면 축소 과정이 제거된다.

<br/>

## The minimum size gotcha
- Flexbox 알고리즘은 자식 요소를 최소 크기 이하로 축소하는 것을 거부한다. 따라서 `flex-shrink`를 이무리 높여도 자식 요소는 더 이상 줄어들지 않고 컨테이너를 넘어간다.
- Flex 자식 요소에 `min-width: 0px`을 설정하면 Flexbox 알고리즘이 '기본 제공' 최소 너비를 덮어쓰도록 지시한다. `0px`로 설정했기 때문에 구성 요소는 원하는 만큼 축소될 수 있다.

<br/>

## Gaps
- `gap`을 사용하면 각 Flex 자식 요소 사이에 공간을 만들 수 있다. 
- `auto margin`은 여분의 공간을 차지하여 구성 요소의 여백에 적용된다. 이를 통해 여분의 공간을 어디에 분배할지 정밀하게 제어할 수 있다.
- 예를 들면 헤더의 한쪽에 로고가 있고 다른 쪽에는 탐색 링크가 있는 경우, 로고 구성 요소에 `margin-right: auto`을 설정해서 구현할 수 있다.

<br/>

## Wrapping
- `flex-wrap: wrap`을 설정하면 항목이 가상 크기 이하로 줄어들지 않고 줄바꿈이 된다.
- 각 `row`는 자체적인 미니 Flexbox 환경이다. 예를 들면 `align-items`는 각 항목을 각 `row`를 감싸는 보이지 않는 상자 내에서 위아래로 이동한다.


