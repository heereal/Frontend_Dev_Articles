# Cursor based Pagination 커서 기반 페이지네이션
> [Cursor based Pagination(커서 기반 페이지네이션)이란? - Querydsl로 무한스크롤 구현하기](https://velog.io/@znftm97/%EC%BB%A4%EC%84%9C-%EA%B8%B0%EB%B0%98-%ED%8E%98%EC%9D%B4%EC%A7%80%EB%84%A4%EC%9D%B4%EC%85%98Cursor-based-Pagination%EC%9D%B4%EB%9E%80-Querydsl%EB%A1%9C-%EA%B5%AC%ED%98%84%EA%B9%8C%EC%A7%80-so3v8mi2)

<br/>

## 페이지네이션이란?
- 전체 데이터에서 지정된 갯수만 데이터를 전달하는 방법으로, 필요한 데이터만 주고 받으므로 네트워크의 오버헤드를 줄일 수 있다.
- 페이지네이션 구현 방법은 두 가지가 있다.
  - 오프셋 기반 페이지네이션 (Offset-based Pagination)
  - 커서 기반 페이지네이션 (Cursor-based Pagination)

<br/>

## 오프셋 기반 페이지네이션
```SQL
select *
from post
order by create_at desc
limit 10, 20;
```
- **페이지 단위로 구분**하는 offset, limit 을 사용한 쿼리 이용 (MySQL 기준)
- 하지만 치명적인 단점이 있다.
   - 새로운 데이터가 생성되었을 경우 데이터를 중복해서 보여주거나 특정 데이터를 건너뛰게 되는 문제가 발생한다.
   - offset 값이 클 때 앞에 있는 모든 데이터를 읽어야 하기 때문에 성능 저하 문제가 발생한다.

<br/>

## 커서 기반 페이지네이션
```SQL
# 첫 페이지 진입시 발생 쿼리
select *
from post 
order by id desc
limit 10;

# 이후 페이지 요청시 발생 쿼리
select *
from post
where id < 10 # ex) cursor값이 10인 경우
limit 10;
```
- Cursor란 사용자에게 응답해준 마지막의 데이터의 식별자 값(주로 id)을 의미하며 **해당 Cursor를 기준으로 다음 n개의 데이터를 응답**해주는 방식이다.
- 오프셋 기반 방식과 다르게 어떤 페이지를 조회하든 항상 원하는 데이터 개수만큼만 읽기 때문에 성능상 이점이 존재한다.

<br/>

## 페이지네이션 방식 비교
- 오프셋 기반 페이지네이션: "1억번~1억+10번 데이터 주세요." → 1억 + 10개의 데이터를 읽는다.
- 커서 기반 페이지네이션: "마지막으로 읽은 데이터(1억번)의 다음 데이터(1억+1번) 부터 10개의 데이터 주세요." → 10개의 데이터만 읽는다.


