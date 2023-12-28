# 비선형 자료구조

## 그래프
    정점과 간선으로 이루어진 자료구조
![그래프](https://velog.velcdn.com/images%2Fcodenmh0822%2Fpost%2Ffb62408e-2cdd-49dc-8b2e-6ea5aa331fc3%2Fimage.png)
- 정점(vertex)
  - 노드(node)라고도 부르며 데이터가 저장되는 공간
- 간선(edge)
  - 링크(link)라고도 부르며 정점간의 관계를 나타낸다
- 특징
  - 정점은 여러 개의 간선을 가질 수 있다.
  - 방향이 없는 무방향 그래프와 방향이 존재하는 방향 그래프로 나눌 수 있다.
  - 간선은 가중치를 가질 수 있다.
  - 사이클이 발생할 수 있다.
  - > 사이클 -> 경로의 시작 정점과 종료 정점이 동일한 경우 ( A에서 출발하여 다시  A로 돌아오는 경우)

## 트리
    그래프의 한 종류로, 트리 구조로 배열된 계층적 데이터 집합
    데이터의 각 요소들은 부모-자식 관계를 가진다.
![트리](https://velog.velcdn.com/images%2Fcodenmh0822%2Fpost%2Fa12e3c90-5f33-4d71-8355-c3a0a3f17798%2Fimage.png)
- 루트 노드(root node)
  - 가장 위에 있는 노드
- 단말 노드 / 리프 노드 (leaf node)
  - 자식이 없는 노드
- 내부 노드(internal node)
  - 단말 노드가 아닌 노드
- 형제 노드(sibling node)
  - 같은 부모를 가지는 노드
- 깊이(depth)
  - 루트에서 어떤 노드에 도달하기 위해 거쳐야 하는 간선의 수
- 특징
  - 트리는 사이클이 존재할 수 없다.
  - 노드가 N개인 트리는 항상 N-1개의 간선을 가진다.

### 이진 트리
    모든 노드의 자식 노드 수가 2개 이하인 트리
![이진트리](https://velog.velcdn.com/images%2Fkkimbj18%2Fpost%2F97908fb6-00b2-4e36-a698-1070cc6f28e1%2Fimage.png)
- 정이진 트리(full binary tree)
  - 자식 노드가 0 또는 두개인 이진 트리
- 완전 이진 트리(complete binary tree)
  - 왼쪽에서부터 채워진 이진 트리
  - 마지막 레벨을 제외하고는 모든 레벨이 완전히 채워져 있다.
- 편향 이진 트리 / 변질 이진 트리(degenerate/skewed tree)
  - 모든 내부 노드는 하나의 자식 노드만 가져야 한다.
  - 사실상 Linked List와 같은 구조
  - BST에서 이 문제로 Red Black Tree가 생겼다.
- 포화 이진 트리(perfect binary tree)
  - 마지막 레벨을 제외한 모든 노드가 2개의 자식 노드를 지니고 있는 트리
  - 노드의 수: 2^h - 1
- 균형 이진 트리(balanced binary tree)
  - 모든 단말 노드 레벨 차가 1보다 작거나 같은 트리
  - Red Black Tree의 최종 목적이 균형 이진트리를 벗어나지 않기 위함.
  - 균형 이진 트리를 위배하는 경우 각 노드 탐색 속도가 저하된다.

### 이진 탐색 트리(Binary Search Tree)
    노드의 왼쪽 하위 트리에는 해당 노드보다 작은 값만 포함되고 오른쪽에는 해당 노드보다 큰 값만 포함되는 이진 트리
- 각 노드는 중복되지 않는 키를 보유
- 좌우 서브트리도 모두 이진 탐색트리여야 한다.
- '검색'에 용이
  - 보통의 경우 O(logn)
  - 최악의 경우 O(n)
      - > 삽입 순서에 따라 선형적인 구조가 될 수 있기 때문.(편향이진트리)  
        > 5->4->3->2->1 순서로 삽입할 시 왼쪽으로만 값이 삽입

### AVL 트리 (Adelson-Velsky and Landis Tree)
    이진 탐색 트리가 최악의 경우 선형 트리가 되는 것을 방지하기 위해 스스로 균형을 잡는 이진 탐색 트리
- 좌 우 서브 트리의 높이 차이가 최대 1
- 높이 차이가 1보다 커지면 회전(Rotation)을 통해 균형을 맞춰 높이 차이를 줄인다.
    #### Balence Factor(BF)
        균형이 무너졌는지 판단하기 위해 활용
        BF(K) = K의 왼쪽 서브트리의 높이 - K의 오른쪽 서브트리의 높이
        -1,0,1 중 하나여야 한다. 벗어나면 균형이 깨졌다는 것 -> 회전이 필요함.
    #### 우 회전 (Right Rotation)
    ![우회전](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FwxXjj%2Fbtro6alLimV%2Fo7oeM9EtG3PDAfNd7Nnlqk%2Fimg.png)
    > 1. y노드의 오른쪽 자식 노드를 z노드로 변경
    > 2. z노드의 왼쪽 자식 노드를 y노드의 오른쪽 서브트리 (T2)로 변경
    #### 좌 회전 (Left Rotation)
    ![좌회전](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbvi2dr%2FbtrpaIoxOIj%2FvbPMbWybCbhmgCqkwLYFg0%2Fimg.png)
    > 1. y노드의 왼쪽 자식 노드를 z노드로 변경
    > 2. z노드의 오른쪽 자식 노드를 y노드의 왼쪽 서브트리 (T2)로 변경
    #### LL(Left Left) Case
    ![LL](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbaSn1R%2FbtrpiIt2dht%2FY3kiKmhWBmyWhPzXlWinzK%2Fimg.png)
    > BF가 적정 값(-1~1)을 벗어난 노드를 기준으로 왼쪽, 왼쪽 노드가 존재한다면 LL Case  
    -> 우회전 적용
    #### RR(Right Right) Case
    ![RR](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F6FueX%2FbtrpcP8N29L%2F0KEPdtSTmitNQD3o9aW2Vk%2Fimg.png)
    > BF가 적정 값(-1~1)을 벗어난 노드를 기준으로 오른쪽, 오른쪽 노드가 존재한다면 RR Case  
    -> 좌회전 적용
    #### LR(Left Right) Case
    ![LR](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FN49KJ%2FbtrpiuWMW3t%2FiyKeW0PbnWYQRuyciwGQd1%2Fimg.png)
    > BF가 적정 값(-1~1)을 벗어난 노드를 기준으로 왼쪽, 오른쪽 노드가 존재한다면 LR Case  
    -> BF에 이상이 있는 노드의 왼쪽 자식노드를 기준으로 좌회전  
    -> 이 후 BF에 이상이 있는 노드를 기준으로 우회전
    #### RL(Right Left) Case
    ![RL](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbT4BgF%2FbtrpaH4eyAO%2FUk8nJOYUCgNoIeKfoUAhN1%2Fimg.png)
    > BF가 적정 값(-1~1)을 벗어난 노드를 기준으로 오른쪽, 왼쪽 노드가 존재한다면 RL Case  
    -> BF에 이상이 있는 노드의 오른쪽 자식노드를 기준으로 우회전  
    -> 이 후 BF에 이상이 있는 노드를 기준으로 좌회전
> 시뮬레이터: https://www.cs.usfca.edu/~galles/visualization/AVLtree.html

### 레드 블랙 트리
    일종의 자기 균형 이진 탐색 트리
    각 노드들은 red or black 색상을 가진다.
![RB Tree](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FsqL0y%2Fbtrw8OzLUUD%2FeQOlslCKoxL7pX8L1MO47K%2Fimg.png)
- 용어
  - NIL node(leaf)
    -  그림의 사각형으로 된 리프 노드
    -  따로 키나 데이터를 포함하지 않고 실제로 구현되지도 않는 "가상의 노드"
   -  internal nodes
      -  NIL이 아닌 나머지 노드
   -  black height 
      -  루트 노드에서부터 리프노드까지 경로에 있는 검은 노드의 개수
-  특징
   -  루트 노드와 모든 NIL 노드들은 항상 블랙 -> Double Red(연속해서 나오는 Red 노드)가 발생하면 안 된다. 
   -  레드 노드의 자식은 모두 블랙
   -  블랙 노드의 자식은 무엇이든 될 수 있다.
   -  루트 노드에서 모든 리프 노드까지의 경로에 대해서 거치는 블랙 노드의 숫자는 같다.
-  삽입 연산
   -  새로 삽입되는 노드의 색은 무조건 <span style="color:red">red</span>
   -  Double Red가 발생하면 다음 두가지 전략 사용
      -  `Recoloring`
         -  새로 삽입된 노드의 삼촌 노드 (부모 노드의 형제 노드)가 Red인 경우
         -  1. 삽입된 노드의 부모와 삼촌을 Black으로 만든 후 조부모를  <span style="color:red">red</span>로 변경
         -  2. 만약 조부모가 루트노드가 아니라면 Double Red가 다시 발생할 수 있다. -> Double Red가 발생한 부분에서 다시 한번 전략 사용
         -  3. 루트노드가  <span style="color:red">red</span>로 변경되면 Black으로 변경하고 종료
      -  `Restructuring`
         -  새로 삽입된 노드의 삼촌 노드가 Black인 경우
         -  1. 삽입된 노드와 부모, 조부모 노드를 오름차순 정렬
         -  2. 가운데 값을 부모로 만든 뒤, 나머지 둘을 자식으로 만든다.
         -  3. 이 때 부모는 Black, 두 자식은  <span style="color:red">red</span>로 만든다.