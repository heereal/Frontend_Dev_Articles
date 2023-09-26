# Command Query Separation

> [영한갓님 JPA 실전 강의 들었는 데 CQS, CQRS 안다, 모른다?](https://velog.io/@xpmxf4/%EC%98%81%ED%95%9C%EA%B0%93%EB%8B%98-JPA-%EC%8B%A4%EC%A0%84-%EA%B0%95%EC%9D%98-%EB%93%A4%EC%97%88%EB%8A%94-%EB%8D%B0-CQS-CQRS-%EC%95%88%EB%8B%A4-%EB%AA%A8%EB%A5%B8%EB%8B%A4)
- **Command**는 객체를 바꾸는 쓰기에 해당
- **Query**는 객체를 변경하지 않고 정보만을 반환
- CQS는 메서드 호출 시 "읽기"와 "쓰기"를 엄격히 분리하는 것
- **CQRS**(Command and Query Responsibility Segregation)는 CQS의 컨셉을 가져오되, 객체를 2가지로 분리하는 디자인 패턴
