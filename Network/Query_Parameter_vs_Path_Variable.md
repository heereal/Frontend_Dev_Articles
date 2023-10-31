# Query Parameter vs Path Variable

![images_kho5420_post_efb41943-dadf-4272-a511-bf4ccbe6b39c_image](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/d2922276-79f2-4120-a010-1be998256274)

## Query Parameter
```javascript
/user?id=123 // id가 123인 유저
/product?price=3000&name=사과 // price가 3000이면서 name이 사과인 상품
/product?offset=0&limit=100 // offset ~ limit 사이의 개수만 출력
```
- URL에 미리 협의된 **데이터를 파라미터를 통해 넘기는 것**을 의미하며, 클라이언트가 어떤 특정 리소스에 접근하고 싶어하는지 서버 측에 추가적인 정보를 전달한다.
- 주로 **정렬이나 필터링**을 할 때 사용한다.
```
/엔드포인트주소?파라미터=값&파라미터=값
```
- 정해진 엔드포인트 주소 이후에 `?`를 쓰는 것으로 쿼리스트링이 시작함을 알린다.
- `=`로 key와 value가 구분된다.

<br/>

## Path Variable
```javascript
/product/1 // product id가 1번인 상품 출력
```
- 경로를 변수로서 사용한다.
- 주로 어떤 **resource를 식별**할 때 사용한다.

<br/>

## References
[When Should You Use Path Variable and Query Parameter?](https://medium.com/@fullsour/when-should-you-use-path-variable-and-query-parameter-a346790e8a6d) / [[번역] Path Variable과 Query Parameter는 언제 사용해야 할까?](https://ryan-han.com/post/translated/pathvariable_queryparam/)   
[[Web] Query Parameter & Path Parameter](https://velog.io/@kho5420/Web-Query-Parameter-Path-Parameter)   
[Query String 쿼리스트링이란?](https://velog.io/@pear/Query-String-%EC%BF%BC%EB%A6%AC%EC%8A%A4%ED%8A%B8%EB%A7%81%EC%9D%B4%EB%9E%80)



