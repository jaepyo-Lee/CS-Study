# B-Tree와 B+Tree

## Tree 구조
<img src="https://github.com/jmxx219/CS-Study/assets/74135929/28675d9b-f9df-4cb2-8f20-d3df9a1ac93b" width="49%">

- Tree구조는 데이터를 계층적으로 표현하는 자료구조이다. 
- 기준에 따라 계층적으로 분류되어있기 때문에 삽입/삭제 수행시 O(logN)시간이 소요된다.
  - 일반적인 Array나 연결리스트 이용해 O(N)이 걸린다.

데이터베이스는 인덱스를 통해 데이터를 분류하고, 삽입/삭제/조회가 많이 일어나는 만큼 Tree구조로 데이터를 관리하기 적합하다.

따라서 데이터베이스는 Tree구조를 적용하는데, 그 중 B-Tree와 B+Tree를 적용하고 있다.

<br/>

## B-Tree

<img src="https://github.com/jmxx219/CS-Study/assets/74135929/f334e7e5-f92b-4d31-a4ab-55a50267ba10" width="49%">

<br>
B-Tree는 이진 트리와 다르게 하나의 노드에 많은 정보를 가지고 있는 형태입니다. 

그림의 파란부분은 각 노드의 key를 나타내며, 빨간부분은 자식 노드를 가르키는 포인터입니다. 

**특징**
- 하나의 노드가 두개 이상의 값을 가질수 있음
  - 최대 자식 수의 개수에 따라 1, 2, 3, .. M차 B-tree가 있음
- 데이터가 정렬된 상태로 유지되어 있음(핵심) 
  - key 값을 이용해 찾고하는 데이터를 트리 구조를 이용해 찾음
- 균형트리이기 때문에 B-tree는 `어떤 값에 대해서도 같은 시간에 결과를 얻을 수 있다`는 `균일성` 장점을 가짐
  
```
균형 트리
- 균형 트리(Balanced-Tree)는 루트 노드부터 리프 노드까지의 거리가 일정한 트리 구조
  - 탐색 성능을 높이기 위해 균형 있게 높이를 유지
- 균형을 유지할 경우, 어떤 데이터를 검색할 때 빠른 속도로 데이터를 찾을 수 있음
- 일반적인 트리인 경우, 탐색하는데 평균적으로 O(logN) 시간 복잡도를 가지지만, 트리가 편향되어 있으면 최악의 시간 복잡도로 O(N)을 가짐
  - 이러한 단점을 보완하기 위해 트리가 편향되지 않도록 항상 밸런스를 유지하는 트리가 필요(균형 트리)
  - 자식들의 밸런스를 잘 유지하면 최악의 경우에도 O(logN) 시간 복잡도를 가짐
- ex) RedBlack-Tree(RBT), B-Tree
```

### B-Tree의 연산
[링크 첨부](https://velog.io/@emplam27/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-B-Tree)

<br/>

## B+Tree
<img src="https://github.com/jmxx219/CS-Study/assets/74135929/f6bffbc0-e811-4f61-b97d-80130d5ff7dc" width="49%">

<br>

B+Tree는 B-Tree에서 개선된 구조로, B-tree와 달리 실제 데이터는 리프노드에만 저장한다.

리프노드들간의 연결되어 있어, 범위 탐색시 B-Tree보다 좋은 성능을 낼 수 있다.

<br>

### B+Tree 특징

- 중복 키를 가짐
  - 내부 노드들이 데이터를 가지고 있지 않기 때문에 리프 노드들이 키와 데이터를 모두 가지고 있어야 함
- 리프 노드를 제외하고 데이터를 담아두지 않기 때문에 메인 메모리를 더 확보해 더 많은 key를 수용할 수 있음
  - 하나의 노드에 더 많은 key들을 담을 수 있기 때문에 트리의 높이는 더 낮아짐
  - cache hit를 높일 수 있음

<br/>

### B-tree와 B+tree의 비교

|   비교    |          B-tree           |          B+tree           |
|:-------:|:-------------------------:|:-------------------------:|
| 데이터 저장  |  모든 내부, 리프 노드들이 데이터를 가짐   |       리프노드만 데이터를 가짐       |
|  검색 속도  |       모든 노드 검색, 느림        |       리프노드에서 선형 탐색        |
|  키 중복   |            없음             |            있음             |
|   삭제    | 내부 노드의 삭제는 복잡하고 트리 변경이 많음 | 어떠한 노드든 리프에 있기 때문에 삭제가 쉬움 |
| 링크드 리스트 |           존재 x            |    리프 노드는 링크드 리스트로 저장됨    |
|   높이    |     특정 갯수의 노드는 높이가 높음     | 같은 노드일 때 B-tree보다 높이가 낮음  |
|   사용    |       데이터베이스, 검색엔진        |     멀티레벨 인덱스, DB 인덱스      |


<br/>

## DB는 여러 자료구조 중에 왜 B-Tree/B+Tree를 사용할까?

#### 자료구조
- 해시테이블
  - 탐색 시간이 제일 빠름
  - 모든 값이 정렬되어 있지 않기 때문에, 해시 테이블에서는 특정 기준보다 크거나 작은 값(부등호)을 찾을 수 없음
  - 따라서 기준 값보다 크거나 작은 요소들을 항상 탐색할 수 있어야 하는 DB 인넥스 용도로는 맞지 않음
  
- RedBlack-Tree(RBT)
  - B-tree와 큰 차이는 `하나의 노드가 가지는 데이터의 개수`
  - RedBlack-Tree는 무조건 하나의 노드에 하나의 데이터 요소만 가지고, B-Tree는 하나의 노드에 여러 개의 데이터 요소를 저장(배열처럼 저장되어 있음)함
    - B-Tree는 같은 노드 상 데이터를 탐색할 때는 포인터 접근이 아닌, 실제 메모리 디스크에서 바로 다음 인덱스의 접근을 함
    - 하지만 RedBlack-Tree는 각 노드마다 무조건 하나의 데이터만 가지기 때문에 데이터를 접근할 때 무조건 참조 포인터로 접근하게 됨

- 배열
  - 참조 포인터라는 개념이 없고, 모든 데이터가 메모리 상 차례대로 저장되어 있어 접근이 매우 빠름
  - 탐색 속도로만 본다면 B-Tree보다 훨씬 빠름
  - 해시 테이블과 다르게 정렬 상태로 유지할 수있어 부등호 연산에도 문제가 없음
  - 하지만 배열이 B-Tree보다 빠른 것은 `탐색`뿐임
    - 배열 내에서 데이터의 저장, 삭제가 일어나는 순간 훨씬 비효율적인 성능이 발생하게 됨

<br/>

**B-Tree의 배열 형식의 접근과 RedBlack-Tree의 참조 포인터 접근**
- 둘다 시간 복잡도는 O(logN)이지만, 이는 알고리즘 처리에 대한 이론적인 시간 계산 방식일 뿐임
  - 물리적, 절대적인 시간 개념으로는 배열 접근이 훨씬 빠름
- 참조 포인터로 접근
  - 참조 포인터로 메모리에 접근하는 것은 실제 메모리상 순서대로 저장이 되었든 안되었든, 접근하려는 주소를 연산을 통해 직접 알아내어야 함
  - 이는 주소를 알아내는데 CPU가 내부적으로 많은 연산을 하게 됨
- 배열 형식의 접근
  - 배열은 데이터들이 메모리 공간에 차례대로 저장되어 있으므로 접근할 주소를 바로 알 수 있음
  - 따라서 메모리 주소를 알아내는데 성능 영향이 없음
  - B-tree도 자식 노드를 접근할 때는 참조 포인터로 접근함
    - 하지만 하나의 노드가 가지는 데이터 개수가 많아질수록 포인터 개수는 확연히 줄어들고, 트리 내에서 데이터가 많아질수록 이러한 차이는 더욱 커짐
- 결국 포인터 접근 수의 차이로 B-Tree가 RedBlack-Tree보다 탐색 시간이 더 빠름

<br/>

#### 데이터베이스 인덱스로 적합한 자료구조인 B-tree
- 항상 정렬된 상태로 특정 값보다 크고 작은 부등호 연산에 문제가 없음
- 참조 포인터가 적어 방대한 데이터 양에도 빠른 메모리 접근이 가능함
- 데이터 탐색뿐만 아니라, 저장, 수정, 삭제에도 항상 O(logN)의 시간 복잡도를 가짐

<br/>

### InnoDB의 B+tree
- MySQL의 DB engine인 InnoDB는 B+tree로 인덱싱을 처리함
- InnoDB에서 사용된 B+tree
  - 같은 레벨의 노드끼리는 Linked List가 아닌 Double Linked List를 사용
  - 자식 노드로는 Single Linked List로 연결되어 있음
  - key의 범위마다 찾아가야할 페이지 넘버(포인터)가 있는데, 해당 페이지 넘버를 통해 곧바로 다음 노드로 넘어감
  - 리프 노드에서 디스크에 존재하는 데이터의 주소값을 구할 수 있고, Linked List 통해 탐색도 가능함
