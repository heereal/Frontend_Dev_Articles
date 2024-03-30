# 이미지 최적화
## 이미지 최적화를 고려해야 하는 이유
1. 사용자 경험 향상
2. 더 나은 페이지 성능
3. 향상된 가시성(visibility): SEO에 이점

<br/>

## 웹 이미지 로딩 속도를 높이는 10가지 방법
1. **Serve correctly sized images**: `srcset` 속성을 사용해서 화면 너비와 같이 특정 조건에 해당할 때만 활성화되는 여러 가지 소스를 전달할 수 있다.
2. **Serve images with modern formats**:  WebP, AVIF 포맷을 사용해서 화질 저하 없이 이미지를 압축해서 전달할 수 있다.
3. **Use an image-optimized CDN**: CDN을 통해 서버에서 이미지를 자동으로 변환해서 최적화를 제공할 수 있다.
4. **Lazy load images**: `loading="lazy"` 속성을 추가해서 이미지가 사용자의 뷰포트에 들어왔을 때만 브라우저가 이미지를 로드하도록 할 수 있다.
5. **Decode images asynchronously**: `decoding="asynchronous"` 속성을 추가해서 이미지를 비동기적으로 디코딩 할 수 있다.
6. **Provide low resolution placeholders**: 이미지 로딩이 완료되기 전에 이미지의 흐릿한 버전을 표시하는 플레이스홀더를 통해 사용자가 인지하는 로딩 시간을 줄여준다.
7. **Cache Images**: HTTP에 `Cache-Control` 헤더를 추가해서 캐시의 유효 기간을 조정할 수 있다.
8. **Define image dimensions**: 이미지의 `width`, `height`를 설정하거나 `aspect-ratio` 속성을 추가하는 방법으로 레이아웃 시프트 현상을 방지할 수 있다.
9. **Layout images lazily with content-visibility**: `content-visibility` 속성을 통해 페이지 로드 시 모든 이미지를 렌더링하지 않고 사용자가 이미지 근처로 스크롤할 때만 이미지를 렌더링하도록 브라우저에 지시한다.
10. **Use SVGs when possible**: SVG 포맷을 사용하면 파일 크기를 줄이고 선명한 이미지를 전달할 수 있다.
    
<br/>

## 이미지 최적화 사례
### img 태그 사용하기
<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/5dd1561c-42bf-46d6-9cdb-b1f7249f6c07" width="500px">

`<img>` 태그는 `srcset`이나 `sizes`와 같은 유용한 최적화 속성을 제공함으로써 더 빠른 페이지 로드를 도와준다.   
`<img>` 태그는 특히 아래와 같은 상황에 적절하다.
- 이미지가 장식의 역할을 할 뿐만 아니라 콘텐츠의 일부일 때.
- 경고 아이콘과 같이 이미지에 중요한 의미가 있고, 이러한 맥락이 스크린 리더와 같은 보조 기구에 잘 전달되기를 원할 때.
- 이미지가 SEO의 이점을 갖기를 원할 때. 구글은 배경 이미지를 자동으로 인덱싱하지 않는다.
- 브라우저에 의존하여 텍스트 크기에 맞게 이미지를 확장하고 렌더링할 때.

<br/>

### 차세대 이미지 형식 활용하기
<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/de01aab6-0d28-4082-8fc9-0ee8ae829188" width="500px">

- 이미지 최적화의 또 다른 좋은 방법은 뛰어난 압축 및 품질을 위해 WebP와 같은 차세대 형식을 이용하는 것이다.
- WebP 이미지는 JPEG이나 PNG보다 파일 크기가 최소 25~30% 작다. WebP 이미지는 기존 형식에 비해 로드 속도가 더 빠를 뿐만 아니라 모바일 데이터를 적게 소모한다.
- 모든 웹 브라우저가 WebP를 지원하지는 않지만 `<source>`와 함께 `<picture>` 태그를 사용하면, 이전 버전과 호환이 되어 모든 브라우저에서 올바르게 최적화된 이미지 형식을 표시할 수 있다.

<br/>

### alt text로 이미지의 접근성 높이기
<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/02168b90-c858-4857-9ea8-f1bbbb07c9c8" width="500px">

- alt 대체 텍스트는 그래픽의 기능과 모양에 대한 정확한 맥락 정보를 제공한다.
- 이는 일반적으로 사용자 경험을 개선할 뿐만 아니라, 장애가 있는 사용자들이 콘텐츠에 접근하도록 돕는 데에도 중요하다. 
- 또한 잘 작성된 alt text는 이미지의 순위를 상승시키고, 웹사이트에 더 많은 사용자를 끌어들인다.

<br/>

### srcset으로 반응형 이미지 생성하기
<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/63223f7c-4305-4470-830b-8a3d68dfc56c" width="500px">

- `srcset` 속성을 사용하면 사용자들의 단말기 화면 너비에 따라서 서로 다른 이미지를 제공할 수 있다.
- `x` 대신에 `w` 단위를 사용하는 게 좋다. `x` 단위는 픽셀의 밀도를 다루기 때문에 고정 크기의 이미지에 더 적합하고, `w` 단위는 화면 너비에 따라 올바른 이미지를 가져온다.

<br/>

### sizes로 비율 조정 지원하기
<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/e8ef2a7d-2d8b-4ae0-9602-b474d9af9438" width="500px">

- `<img>`태그에 `sizes` 속성을 명시하면 이미지의 너비가 몇 픽셀인지 브라우저에 미리 알려줄 수 있다.
- `px`로 이미지의 절대 너비를 제공하는 대신에, `vw` 단위를 사용하여 화면에서 차지할 예상 비율을 지정할 수도 있다.

<br/>

### 가로세로 비율 보존하기
<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/e25e6453-df6a-4ee3-8ac5-c3dd5d2fedd3" width="500px">

- 이미지를 최적화하지 않으면 예상치 못한 레이아웃 시프트(layout shift) 현상이 발생할 수 있다.
- HTML에서 이미지의 너비와 높이를 지정하고, CSS에서 `height: auto`로 설정하면 레이아웃 시프트 현상을 최소화할 수 있다. 
- 추가로 CSS의 `object-fit` 속성을 사용하면 이미지가 페이지를 채우거나, 덮거나, 포함되거나, 축소되어야 하는지를 브라우저에 알려줄 수 있다.

<br/>

### 중요 이미지는 fetchpriority로 빠르게 로드하기
<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/b37b383f-29d2-4468-98b7-8d649d4572bb" width="500px">

- `fetchpriority="high"` 를 사용하면 우선순위가 높은 이미지를 우선적으로 처리해야 한다고 브라우저에 알려줄 수 있기 때문에 브라우저는 다른 이미지에 자원을 즉시 소비할 필요가 없다.

<br/>

### 지연 로딩(lazy loading)과 async decoding으로 성능 높이기
<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/cc760730-348d-4b5d-857a-2ad5b627cedb" width="500px">

- `loading="lazy"`를 사용하면 사용자들이 스크롤 하기 전까지 웹 페이지에 직접적으로 보이지 않는 모든 것은 우선순위에서 밀려난다.
- `decoding="async"`를 사용해서 화면 하단의 LCP가 아닌 이미지에 대해 디코딩을 먼저 할 필요가 없도록 지정할 수 있다.

<br/>

## Recap
![image](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/30d66cf0-2d8a-43c1-8ef4-9c8272ea7a81)

<br/>

## Reference 
- [Optimal Images in HTML](https://www.builder.io/blog/fast-images?_host=www.builder.io) / [[번역] 이미지 최적화에 대한 명확한 가이드](https://velog.io/@sehyunny/the-definitive-guide-to-image-optimization)
- [10 ways to speed up web image loading](https://byteofdev.com/posts/speed-up-image-loading/?utm_source=oneoneone)
