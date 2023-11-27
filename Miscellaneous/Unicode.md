# 유니코드

## 유니코드란?
- 유니코드는 **전세계의 모든 문자를 컴퓨터에서 일관되게 표시할 수 있는 산업 표준 코드**이다. (글자와 코드가 1:1로 매핑되어 있는 표준화된 테이블이라고 생각하면 쉽다.)
- `U+0000~U+007F`는 로마자, `U+AC00~U+D7AF` 한글 음절 등 `U+숫자` 형태로 이루어져 있다.
- 1988년 초안이 출판된 이후로, 포함되는 문자가 점점 늘어 가고 있다. 2021년 기준 14.0버전이 나왔고, 159개의 언어 종류(144,697개의 문자)가 포함되어 있다.

<br/>

## UTF (Unicode Transformation Format)
- 유니코드의 각 문자마다 인덱스가 정해져 있다.
- 보통 `UTF-8`의 방식으로 문자를 인코딩한다. 문자마다 적절한 바이트 수를 차지하기 때문에 다른 방식들보다 적은 용량을 차지하면서 호환 문제가 적다.
- `UTF-8`은 `8bit(1byte)` 단위로 인코딩되며, 영어와 숫자 같이 자주 활용되는 문자들은 `1byte`를 할당하고, 특수문자와 고대문자 같이 잘 사용되지 않는 문자들에는 `4byte`를 할당하는 등 **가변 바이트**를 활용한다.
  
![images_goggling_post_f187efc3-af3c-426d-8679-260ae55d4c8d_image](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/5fd2d563-2ba0-4912-8fb0-1bf57aefa999)
- 위와 같이 유니코드의 범위에 따라 `UTF-8` 인코딩의 btye 갯수가 정해진다.

<br/>

## 인코딩 방법
<img width="555" alt="images_goggling_post_b2a72b5e-a9aa-4866-8991-e4eabcf8b0cc_UTF8_곰" src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/35dcfa46-8cef-4e43-ae66-20be7ab1ce7b">

- "곰"은 `U+ACF0`이므로 , 표에서 `3byte` 범위에 속한다.

<img width="537" alt="images_goggling_post_add8c204-efaa-4b20-9881-31c63f510bae_UTF8_a" src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/19f505a0-7d61-45b8-bd2e-4fb4d6b3a526">

- "a"는 `U+0061`이므로, `1byte` 범위에 속한다.

<br/>

## Reference
- [유니코드와 UTF 이해하기](https://velog.io/@goggling/%EC%9C%A0%EB%8B%88%EC%BD%94%EB%93%9C%EC%99%80-UTF-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0)
