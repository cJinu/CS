# Join Kind & Join Priciple

## Join이란?
 조인이란 하나의 테이블이 아닌 두 개 이상의 테이블을 묶어서 하나의 결과물을 만드는 것
 > MySQL 에선 Join, MongoDB 에서는 LookUp이라 한다.

참고로 MongoDB는 NoSql로 RDBMS보다 Join의 성능이 떨어지기 때문에 Join 작업이 많을 경우에는 RDBMS를 사용하는 것을 권장한다.

그렇다면 왜 NoSql은 RDBMS보다 Join의 성능이 떨어질까?

### 1. 데이터 모델의 차이
RDBMS는 정규화된 테이블 구조를 가지고 있어 데이터가 여러 테이블에 분산되어 저장됩니다. JOIN 연산은 이러한 테이블 간의 관계를 복원하고 필요한 데이터를 결합하는 과정을 거칩니다.
NoSQL 데이터베이스는 일반적으로 더 유연한 스키마를 가지고 있거나 스키마가 없는 경우가 많습니다. 데이터는 중첩된 문서나 다른 형태로 저장되기 때문에 JOIN 연산이 필요 없을 수 있습니다.

### 2. 수평 분할(Horizontal Partitioning)
NoSQL은 대부분의 경우 데이터를 수평으로 분할하여 여러 노드에 분산 저장합니다. 이는 확장성을 높이지만, JOIN 연산을 어렵게 만들 수 있습니다. JOIN이 여러 노드 간에 데이터를 조합해야 할 경우, 이로 인해 성능이 저하될 수 있습니다.

### 3. 인덱스의 부재
NoSQL은 일부 경우에는 인덱싱을 제공하지만, RDBMS에서처럼 강력한 인덱스 기능을 제공하지 않는 경우가 있습니다. JOIN 연산을 위해서는 적절한 인덱스가 필요한데, 이 부재로 인해 NoSQL에서는 JOIN이 더 느릴 수 있습니다.

## 조인의 종류
1. 내부조인 (inner join)
```
SELECT * FROM
A JOIN B ON a.id = b.id
```
![image](https://github.com/cJinu/CS/assets/94429120/b8175564-9d9d-4838-8303-664affa7bf01)
![image](https://github.com/cJinu/CS/assets/94429120/8b9b1ff0-d200-4c2d-b290-701a4f0d75e9)

2. 왼쪽 조인 (left join)
```
SELECT * FROM
A LEFT JOIN B ON a.id = b.id
```
![image](https://github.com/cJinu/CS/assets/94429120/98b09846-38aa-4821-abb8-c74437d28d97)
![image](https://github.com/cJinu/CS/assets/94429120/253bc0d2-2ac5-4ab4-a352-d6ed098744d8)

3. 오른쪽 조인 (right join)
```
SELECT * FROM
A RIGHT JOIN B ON a.id = b.id
```
![image](https://github.com/cJinu/CS/assets/94429120/8af373b3-c14e-4ee4-876c-f07e5b82a83f)
![image](https://github.com/cJinu/CS/assets/94429120/840ceb29-49a1-4f2a-8e28-ba8589a2648b)


4. 합집합 조인 (full outer join)
```
SELECT * FROM
A FULL OUTER JOIN B ON a.id = b.id 인 줄 알았으나... MYSQL에서는 full outer join을 지원하지 않는다. 그래서... 아래와 같이 LEFT JOIN과 RIGHT JOIN을 UNION 하는 방식을 사용하기도 한다.
```

```
SELECT *
FROM A
LEFT JOIN B
ON A.id = B.id
UNION
SELECT * 
FROM A
RIGHT JOIN B
ON A.id = B.id;
```
![image](https://github.com/cJinu/CS/assets/94429120/60acf3c8-f171-4c42-97dd-a9549352392c)
![image](https://github.com/cJinu/CS/assets/94429120/36308ec3-a71f-47eb-a491-a30c1121517d)

위의 다이어그램을 직접 실행해보고 싶다면..
https://sql-joins.leopard.in.ua/
## 조인의 원리
앞서 설명한 조인의 종류를 기반으로 조인의 원리를 알아보도록 합시다.

### 중첩루프조인(NLJ, Nested Loop Join)
중첩 for문과 같은 원리로 조건에 맞는 테이블을 서치하는 방법<br>
랜덤 접근에 대한 비용이 많이 증가하기 때문에 대용량 테이블에서는 적합하지 않은 방법이다.<br>
조회의 범위가 좁을때 유리한 방식

### 정렬 병합 조인
각각의 테이블을 조인할 필드 기준으로 정렬하고 정렬이 끝난 이후에 조인 작업을 수행하는 조인 <br>
1. 조인할 적절한 인덱스가 없을 때
2. 대용량의 자료를 조인할때
3. 조인 조건으로 <, =, > 와 같은 범위 비교 연산자가 사용될때
이러할때 주로 사용이 됌

### 해시 조인
해시 테이블을 기반으로 조인하는 방법 <br>
두개의 테이블을 조인 했을 때 하나의 테이블이 메모리에 온전히 들어간다면 중첩루프조인보다 성능이 우수하다. <br>
또한 해쉬 함수를 적용한 값을 통해 조인을 하기 때문에 동등(=)조인에만 사용될 수 있다.

### 수행방식
![image](https://github.com/cJinu/CS/assets/94429120/8bb5eff6-c52b-4d25-8e97-e261286c40c1)
1. 입력 테이블 중 가장 크기가 작은 테이블을 선행 테이블이라고 하며 조인 조건에 맞는 값을 찾는다.
2. 해시 함수를 적용하여 해시 테이블을 만든다.
3. 후행 테이블에서 조인 조건에 맞는 값을 찾는다.
4. 해시 함수를 적용해서 2번에서 생성된 해시 테이블과 같은 값을 찾는다.
5. JOIN을 수행 성공하면 추출버퍼에 넣는다.
6. 후행 테이블의 조건에 만족하는 모든 행에 대해서 3~5번을 반복한다.