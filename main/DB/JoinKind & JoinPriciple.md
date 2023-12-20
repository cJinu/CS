# Join Kind & Join Priciple

## Join이란?
 조인이란 하나의 테이블이 아닌 두 개 이상의 테이블을 묶어서 하나의 결과물을 만드는 것
 > MySQL 에선 Join, MongoDB 에서는 LookUp이라 한다.

참고로 MongoDB는 NoSql로 RDBMS보다 Join의 성능이 떨어지기 때문에 Join 작업이 많을 경우에는 RDBMS를 사용하는 것을 권장한다.

NoSQL이란? 동호형이 정리해줬을것임

## 조인의 종류
1. 내부조인 (inner join)
2. 왼쪽 조인 (left join)
3. 오른쪽 조인 (right join)
4. 합집합 조인 (full outer join)

## 조인의 원리
앞서 설명한 조인의 종류를 기반으로 조인의 원리를 알아보도록 합시다.

### 중첩루프조인(NLJ, Nested Loop Join)
중첩 for문과 같은 원리로 조건에 맞는 테이블을 서치하는 방법<br>
랜덤 접근에 대한 비용이 많이 증가하기 때문에 대용량 테이블에서는 적합하지 않은 방법이다.