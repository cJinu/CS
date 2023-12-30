# 세그먼트 트리

- 여러 개의 데이터가 연속적으로 존재할 때 특정한 범위의 데이터의 연산이 필요할 때 사용하는 자료구조(알고리즘)

## 단순 배열 vs 세그먼트 트리

특정 범위의 합을 구할 때

- 단순 배열(선형적): O(N)
- 세그먼트 트리: O(logN)

## 세그먼트 트리 만들기

![image](https://github.com/cJinu/CS/assets/38110757/cf84bc26-b9a2-4392-b18a-329dc873df35)

- 리프 노드: 배열의 그 수 자체
- 다른 노드: 왼쪽 자식과 오른쪽 자식의 합을 저장

![image](https://github.com/cJinu/CS/assets/38110757/c6cc17b5-4912-441d-9e62-807921db6567)

- 어떤 노드의 번호가 x일때, 왼쪽 자식의 번호는 2*x, 오른쪽 자식의 번호는 2*x+1 ← 이진트리이기 때문!
  - 루트 노드의 번호는 1이어야함! → 중요!!!
- 세그먼트 트리를 만드는데 필요한 배열의 크기를 구하기 위해 우선 높이 먼저 구해야함!
  - 높이 $H=ceil(logN)$
  - 배열의 크기 = $2^{H+1}-1$

```java
int init(int start, int end, int node) {
	// node가 리프 노드인 경우
	if (start == end) return tree[node] = arr[start];

	int mid = (start + end) / 2;

	// 왼쪽 자식: node * 2, 오른쪽 자식: node * 2 + 1
	return tree[node] = init(start, mid, node * 2) + init(mid + 1, end, node * 2 + 1);
}
```

## 합 찾기

- 3 ~ 9 구간의 합을 구하는 경우

![image](https://github.com/cJinu/CS/assets/38110757/6363749c-c1da-41c7-93d7-071f62b3fd25)

```java
int sum(int node, int start, int end, int left, int right) {
	if (left > end || right < start) return 0;
	if (left <= start && end <= right) return tree[node];

	int mid = (start + end) / 2;

	return sum(node * 2, start, mid, left, right) + sum(node * 2 + 1, mid + 1, end, left, right);
}
```

## 수 변경하기

- 5를 변경하는 경우

![image](https://github.com/cJinu/CS/assets/38110757/b7b0d4d0-fded-4056-9a14-ace108121889)

```java
void update(int node, int start, int end, int index, int diff) {
	if (index < start || index > end) return;

	tree[node] += diff;

	if (start != end) {
		int mid = (start + end) / 2;
		update(node * 2, start, mid, index, diff);
		update(node * 2 + 1, mid + 1, end, index, diff);
	}
}
```

# Set과 Map

# Set

- 수학에서의 유한 집합을 구현한 것
- 대상 원소가 집합에 소속되었는지 여부를 검사
- 데이터를 비순차적으로 저장할 수 있는 순열 자료구조
- 삽입한 데이터가 순서대로 저장되지 않음
- 중복해서 삽입이 불가능. 동일한 값이 삽입되면 하나의 값만 저장됨
- Fast Lookup

```java
import java.util.*;

// 객체 선언 - Set은 인터페이스
Set<String> set = new HashSet<>();

// 데이터 삽입
set.add("apple");
set.add("banana");

// 데이터 삭제
set.remove("apple");

// 반복자를 이용한 데이터 출력
Iterator<String> iter = set.iterator();
while(iter.hasNext()) {
	System.out.println(iter.next());
}

// 데이터 포함 유무 - boolean 타입 리턴
System.out.println(set.contains("apple"));

// set 초기화
set.clear();

// 비어있는 set인지 확인 - boolean 타입 리턴
System.out.println(set.isEmpty());

// set 크기
System.out.println(set.size());
```

## HashSet vs TreeSet

- HashSet: 정렬 X, 추가와 삭제에 용이
- TreeSet: 자동 정렬, 이진 탐색 트리로 이루어져 있어 정렬 및 검색에 높은 성능, 추가와 삭제는 시간이 조금 더 걸림

# Map

- key-value 방식: 키와 값을 하나의 쌍으로 저장
- key를 통해 value를 얻어냄
- 요소의 저장 순서 유지 X
- key는 중복을 허용 X, value는 중복 허용

```java
import java.util.*;

// 객체 선언
Map<String, String> map = new HashMap<>();

// 데이터 삽입
map.put("시계", "watch");
map.put("방수포", "tarp");

// 데이터 출력
System.out.println(map.get("시계"));

// 키 유무 확인 - boolean 타입 리턴
System.out.println(map.containsKey("시계"));

// 데이터 삭제 - 삭제 후 value 리턴
System.out.println(map.remove("시계"));

// Map 데이터 개수 리턴
System.out.println(map.size());
```
