# IntersectionObserver
> [실무에서 느낀 점을 곁들인 Intersection Observer API 정리](https://velog.io/@elrion018/%EC%8B%A4%EB%AC%B4%EC%97%90%EC%84%9C-%EB%8A%90%EB%82%80-%EC%A0%90%EC%9D%84-%EA%B3%81%EB%93%A4%EC%9D%B8-Intersection-Observer-API-%EC%A0%95%EB%A6%AC)

<br/>

## IntersectionObserver API란?
- Intersection Observer API 는 루트 요소와 타겟 요소의 교차점을 관찰하여 **타겟 요소가 루트 요소와 교차하는지 아닌지를 구별하는 기능을 제공**한다.
- 스크롤 시 짧은 시간 내에 수 백, 수 천의 이벤트가 동기적으로 실행되는 scroll 이벤트와 다르게 교차 시 비동기적으로 실행되며 가시성 구분 시 reflow 를 발생시키지 않는다.

<br/>

## IntersectionObserver API 사용 방법
```javascript
let options = {
	root: document.querySelector('#scrollArea'), // 루트 요소
	rootMargin: '0px', // 루트 요소의 범위를 확장
        threshold: 1.0 // 타켓 요소가 어느 정도 보여졌을 때 콜백 함수를 호출할지
}

let callback = (entries, observer) => {
  entries.forEach(entry => {
    // 각 entry는 가시성 변화가 감지될 때마다 발생하고 그 context를 나타낸다.
    // 타겟 요소가 루트 요소와 교차하는 점이 없으면 콜백을 호출했으되, 조기에 탈출한다.
    if (entry.intersectionRatio <= 0) return
    // ... 콜백 로직
  });
};

// options에 따라 인스턴스 생성
let observer = new IntersectionObserver(callback, options);

// 타겟 요소 관찰 시작
let target = document.querySelector('#listItem');
observer.observe(target);
```
- new 키워드를 통해 인스턴스를 생성하며 callback , options 2개의 파라미터를 받는다.
- `callback`은 가시성의 변화가 생겼을 때 호출되는 콜백 로직이다.
- `options`는 만들어질 인스턴스에서 콜백이 호출되는 상황을 정의한다.

<br/>

## IntersectionObserver API 사용 예시
- 페이지가 스크롤 되는 도중에 발생하는 이미지나 다른 컨텐츠의 레이지 로딩
- 무한스크롤을 구현
- 광고 수익을 계산하기 위한 용도로 광고의 가시성 보고
- 사용자에게 결과가 표시되는 여부에 따라 작업이나 애니메이션을 수행할 지 여부를 결정




