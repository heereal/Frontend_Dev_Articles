# SVG

## PNG를 사용할 경우 문제점
- 유저들에게 완벽한 이미지를 제공하기 위해서는 해상도에 따라 3가지 타입의 디스플레이를 가진 디바이스를 지원해야 한다.
- 이로 인해 디스플레이마다 1x, 2x, 3x의 이미지를 각각 관리해야 하는 문제가 발생한다.

<br/>

## SVG(Single Vector Image)의 등장
<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/c43277ba-d047-49ce-b1fa-6c3a2b4ae51d" width="300px">

- SVG는 `XML`로 구성되어 있다. 그렇기 때문에 어떤 사이즈로 변환을 해도 그래프가 깨지지 않으며 SVG 파일을 개발자가 직접 수정할 수도 있다.
- SVG를 사용하면 관리해야 할 이미지 asset의 개수와 용량이 확연하게 줄어든다. 즉, **하나의 SVG 파일로 모든 사이즈에 대응**할 수 있는 것이다.
- 또한 SVG는 PNG에 비해 용량을 적게 차지하는 장점도 있다.

<br/>

## SVG 사용 시 주의사항
- Xcode 12부터 SVG를 지원하기 때문에 내가 사용하는 Xcode의 버전을 확인해야 한다.
- iOS 13, iPadOS 13, macOS 10.15 버전 이상부터 SVG를 지원한다.
- SVG에는 수학적 계산이 요구되기 때문에 너무 복잡한 이미지의 경우 파일의 크기가 커질 수 있어 오히려 PNG로 처리하는 것이 더 유리하다.
- SVG는 color depth가 제한적이다. 따라서 정확한 이미지 색을 표현하기 위해서는 PNG를 사용하는 것이 더 효율적일 수 있다.
- Xcode에서 SVG를 사용할 때 Gradient가 표현되지 않는 버그가 발생할 가능성이 있다.
- SVG의 특성상 하나의 asset을 여러 사이즈로 변환하여 쓰게 되는데, `Preserve Vector Data`를 체크하지 않으면 SVG를 높은 사이즈로 변환 시 이미지가 깨질 수 있다.

<br/>

## PNG과 SVG 비교 요약
![image](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/484a7955-888d-4151-b15e-d2e724409f9a)


<br/>

## Reference
- [SVG는 진짜 정답일까? 그럼 PNG는?](https://yozm.wishket.com/magazine/detail/2252/?utm_source=oneoneone)
