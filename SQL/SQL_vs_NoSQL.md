# SQL vs NoSQL

## SQL (Structured Query Language)
- SQL을 사용하면 **RDBMS(관계형 데이터베이스)** 에서 데이터를 저장, 수정, 삭제 및 검색 할 수 있다.
- 관계형 데이터베이스는 데이터가 **정해진 데이터 스키마에 따라 테이블에 저장**되고, **관계를 통해 여러 테이블에 분산**된다는 특징이 있다.
- 데이터는 테이블에 레코드로 저장되는데 각 테이블마다 명확하게 정의된 구조가 있기 때문에 스키마를 준수하지 않은 레코드는 테이블에 추가할 수 없다.
- 즉, 스키마를 수정하지 않는 이상은 **정해진 구조에 맞는 레코드만 추가할 수 있다**는 것이 관계형 데이터베이스의 특징이다.
- **수직적 확장**을 통해 데이터베이스 서버의 성능을 향상시킨다. (ex. CPU 업그레이드)

<br/>

## SQL의 장단점
### 장점
- 명확하게 정의된 스키마를 통해 데이터의 무결성을 보장한다.
- 각 **데이터를 중복 없이 한 번만 저장**한다. 따라서 데이터를 수정할 때 한번만 수정하면 된다.

### 단점
- 데이터 스키마를 계획한 후 수정이 불가능하기 때문에 유연성이 떨어진다.
- 테이블마다 관계를 맺고 있기 때문에 JOIN문이 많은 복잡한 쿼리가 만들어질 수 있다.
- 대체로 수직적 확장만 가능하다.

<br/>

## SQL 기반의 관계형 데이터베이스를 사용하는 케이스
- 데이터가 변경될 여지가 없고 명확한 스키마가 데이터와 사용자에게 중요한 경우
- 관계를 맺고 있는 데이터가 자주 변경되는 경우 (NoSQL에서는 여러 컬렉션의 데이터를 모두 수정해야 하기 때문에 비효율적이다.)

<br/>

## NoSQL (Not Only SQL)
- NoSQL에서는 **다른 구조의 데이터를 같은 컬렉션에 추가**할 수 있다.
- **수평적 확장**을 통해 데이터베이스 서버를 추가 및 분산한다. (하나의 데이터베이스가 여러 호스트에서 작동한다.)

<br/>

## NoSQL의 장단점
### 장점
- 스키마가 없기 때문에 **언제든지 저장된 데이터를 조정하고 새로운 필드를 추가할 수 있다**.
- 데이터는 애플리케이션이 필요로 하는 형식으로 저장되기 때문에 데이터를 읽어오는 속도가 빨라진다.
- 수평적 확장을 통해 보다 저렴한 비용으로 서버를 증설할 수 있다.

### 단점
- 유연성으로 인해 데이터 구조 결정을 미루게 될 수 있다.
- **데이터가 여러 컬렉션에 중복**되어 있기 때문에 수정 시 모든 컬렉션에서 수정해야 한다.

<br/>

## NoSQL 기반의 비관계형 데이터베이스를 사용하는 케이스
- 정확한 데이터 구조를 알 수 없거나 데이터의 구조가 자주 변경될 수 있는 경우
- 막대한 양의 데이터를 다루는 등 데이터베이스를 수평으로 확장해야 하는 경우

<br/>

## Reference
- [SQL과 NOSQL의 차이](https://gyoogle.dev/blog/computer-science/data-base/SQL%20&%20NOSQL.html)