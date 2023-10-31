# 페이지 로드 속도를 높이기 위해 GIF를 video로 대체하기
> [Replace animated GIFs with video for faster page loads](https://web.dev/articles/replace-gifs-with-videos?hl=en)   
> [[번역]페이지 로드 속도를 높이기 위해 애니메이션 GIF를 동영상으로 대체합니다.](https://web.dev/articles/replace-gifs-with-videos?hl=ko)

<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/ccd496a4-66b0-478e-bacd-8eace5643320" width="800px">

-  대용량 GIF를 동영상으로 변환하면 사용자의 대역폭을 크게 절약할 수 있다.
-  `Lighthouse`를 사용하여 성능을 체크했을 때에도 GIF가 있는 경우 '애니메이션 콘텐츠에 동영상 형식을 사용'하라는 제안이 표시된다.
  
<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/8698749b-3e25-4479-886d-f136a555d8b4" width="500px">

- 실제로 용량을 비교해봤을 때 GIF와 동영상 간의 비용 절감 효과가 상당히 크다는 것을 알 수 있다.

<br/>

```javascript
<video autoplay loop muted playsinline>
  <source src="my-animation.webm" type="video/webm">
  <source src="my-animation.mp4" type="video/mp4">
</video>
```
- `<video>` 요소를 이용해서 자동으로 재생되고, 끝없이 반복되고, 오디오를 재생하지 않으며, 인라인으로 (전체 화면이 아님) 재생되는 GIF에 요구되는 모든 특성을 대체할 수 있다.
- `<video>` 요소에는 브라우저의 형식 지원에 따라 브라우저에서 선택할 수 있는 여러 동영상 파일을 가리키는 하나 이상의 `<source>` 하위 요소가 필요하다.
- 브라우저는 최적의 `<source>`를 추측하지 않으므로 `<source>`의 순서가 중요하다. 예를 들어 MP4 동영상을 먼저 지정하고 브라우저에서 WebM을 지원하는 경우, 브라우저에서 WebM <source>을 건너뛰고 MPEG-4를 대신 사용한다.
