# Binary Heap

자료구조의 일종으로 Tree의 형식을 하고 있으며 Tree 중에서도 배열에 기반한 __Complete Binary Tree__ 이다. 배열에 트리의 값들을 넣어줄 때, 0 번째는 건너뛰고 1번  index 부터 루트노드가 시작된다. 이는 노드의 고유번호 값과 배열의 index를 일치시켜 혼동을 줄이기 위함이다. __힙(Heap)__에는 __최대힙(max heap)__ , __최소 힙(min heap)__ 두종류가 있다.

- Max heap : 각 노드의 값이 해당 children의 값보다 __크거나 같은__ __complete binary tree__를 말한다.
- max heap에서는 Root node에 있는 값이 제일 크므로, 최대값을 찾는데 소요되는 연산의 시간복잡도는 O(1) 이다. 그리고 __complete binary tree__이기 때문에 배열을 사용하여 효율적으로 관리할 수 있다. 하지만 heap의 구조를 계속 유지하기 위해서는 제거된 루트 노드를 대ㅔ할 다른 노드가 필요하다. 여기서 heap은 맨 마지막 노드를 루트 노드로 대체시킨 후, 다시 heapify 과정을 거쳐 heap 구조를 유지한다. 이런 경우에는 O(log n)의 시간복잡도로 최대값 또는 최소값에 접근할 수 있게 된다.



#### Personal Recommendation

- Heapify 구현하기





# Red Black Tree

RBT(Red-Black Tree)는 BST를 기반으로하는 트리 형식의 자료구조이다. 

Red-Black Tree에 데이터를 저장하게 되면 Search, Insert, Delete에 O(log n)의 시간 복잡도가 소요됨. 동일한 노드의 개수일 때, depth를 최소화하여 시간 복잡도를 줄이는 것이 핵심 아이디어이다. 동일한 노드의 개수일 때, depth 가 최소가 되는 경우는 tree가 complete binary tree인 경우이다.

#### Red-Black Tree의 정의

1. 각 노드는 __Red__ or __Black__ 이라는 색깔을 갖는다.
2. Root node의 색깔은 __Black__ 이다.
3. 각 leaf node는 __Black__이다.
4. 어떤 노드의 색깔이 __red__라면 두 개의 children의 색깔은 모두 black이다.
5. 각 노드에 대해서 노드로부터 descendant leaves 까지의 단순 경로는 모두 같은 수의 black nodes 들을 포함하고 있다. 이를 해당 노드의 __Black-Height__라고 한다. 



#### Red-Black Tree의 특징

1. Binary Search Tree 이므로 BST의 특징을 모두 갖는다.
2. Root node 부터 leaf node 까지의 모든 경로 중 최소 경로와 최대 경로의 크기 비율은 2보다 크지 ㅇ낳다. 이러한 상태를 __balanced__상태라고 한다.
3. 노드의 child가 없을 경우 child를 가리키는 포인터는 NIL 값을 저장ㅎ나다. 이러한 NIL 들을 leaf node로 간주한다.



#### 삽입 & 삭제

- 삽입
  - BST의 특성을 유지하면서 노드를 삽입한다. 그리고 삽입된 노드의 색깔을 __RED__로 지정한다. Red로 지정하는 이유는 Black-Height 변경을 최소화 하기 위함! 삽입 결과 RBT의 특성 위배시 노드의 색깔을 조정하고, Black-Height 가 위배되었다면 rotation을 통해 height를 조정. 이러한 과정을 통해 RBT의 동일한 height에 존재하는 internal node들의 Black-height가 같아지게되고 최소 경로와 최대 경로의 크기 비율이 2 미만으로 유지
- 삭제
  - 삭제될 노드의 child의 개수에 따라 rotation 방법이 달라지게 됨. 그리고 만약 지워진 노드의 색깔이 Black 이라면 Black-Height가 1 감소한 경로에 black node 가 1개 추가되도록 rotation 하고 노드의 색깔을 조정한다. 지워진 노드의 색깔이 red 라면 특성위배가 발생하지 않으므로 RBT가 그대로 유지.



# Hash Table

__hash__ 는 내부적으로 __배열__을 사용하여 데이털르 저장하기 때문에 빠른 검색속도를 갖음.

특정한 값을 seach하는데 데이터 고유의 인덱스로 접근하게 되므로 average case에 대하여 시간 복잡도가 O(1) 이 된다. 하지만 인덱스로 저장되는 key값이 불규칙하다는 문제가 있다.

=> __특별한 알고리즘__을 이용하여 저장할 데이터와 연관된 __고유의 숫자를 만들어 낸 뒤__ 이를 인덱스로 사용. 그 인덱스는 그 데이터만의 고유한 위치이기 때문에 삽입이나 삭제시 추가적인 비용이 없도록 만들어진 구조이다.



#### Hash Function

'특별한 알고리즘' 이란 ? 고유한 인덱스 값을 설정하는 것이 중요해 보임.

위에서 언급한 '특별한 알고리즘'을 __hash method__ 또는 __해시 함수(hash function)__ 라고 하고 이 메소드에 의해 반환된 데이터의 고유 숫자 값을 __hashcode__라고 한다. 저장되는 값들의 key 값을 __hash function__을 통해 __작은 범위의 값들로__ 바꿔준다.

어설픈 function은 동일한 key 값에 복수 개의 데이터가 존재할 수 있게 되는 __Collision__이 발생한다.

=> 그렇다면 좋은 hash function은 어떠한 조건을 갖춰야 하는가?

일반적으로 좋은 __hash function__은 키의 일부분을 참조하여 해쉬 값을 만들지 않고 키 전체를 참조하여 해쉬 값을 만들어냄.

__hash function__를 무조건 1:1로 만드는 것보다 Collision을 최소화 하는 방향으로 설계하고 발생하는 Collision에 대비해 어떻게 대응할 것인가가 더 중요! 1:1 대응이 되도록 만드는 것이 거의 불가능 하기도 하지만 그런 hash function은 array와 다를바 없고 메모리를 너무 차지하는 문제가 있다.

Collsion이 많아질 수록 Search에 필요한 시간 복잡도가 O(1) 에서 O(n)에 가까워 짐. 어설픈 hash function 은 hash 를 hash 답게 사용하지 못하도록 함.

따라서 hashing된 인덱스에 이미 다른 값이 들어 있다면 새 데이터를 저장할 다른 위치를 찾은 뒤에야 저장할 수 있는 것이다.



#### Resolve Confilct

1. Open Address 방식(개방주소법)
   - 해쉬 충돌이 발생하면 __다른 해시버킷에 해당 자료를 삽입하는 방식__이다. 버킷이란 바구니와 같은 개념으로 데이터를 저장하기 위한 공간이라 생각하면 된다.
   - 공개 주소 방식이라고도 불리는 이 알고리즘은 Collision이 발생하면 데이터를 저장할 장소를 찾아헤멘다. 최악의 경우 비어있는 버킷을 찾지 못하고 탐색을 시작한 위치까지 되돌아 올 수 있다. 이 과정의 다양한 방법중 3가지에대해 알아보자.
     - Linear Probing : 순차적으로 탐색하며 비어있는 버킷을 찾을 때 까지 계속 진행
     - Quadratic Probing : 2차 함수를 이용해 탐색할 위치를 찾는다.
     - Double hashing probing : 하나의 해쉬 함수에서 충돌이 발생하면 2차 해쉬 함수를 이용해 새로운 주소를 할당한다. 위 두가지 방법에 비해 많은 연산량을 요구
2. Separate Chaining 방식(분리 연결법)
   - 일반적으로 Open Addressing보다 빠르다. Open Addressing 경우 해시 버킷을 채운ㅇ 밀도가 높아질수록 최악의 상황 빈도가 높아지기 때문. 하지만 Separate Chaining 방식의 경우 해시 충돌이 잘 발생하지 않도록 보조해서 함수를 통해 조정할 수 있다면 Worst Case에 가가워 지는 빈도를 줄일 수 잇음. 
     - 연결 리스트를 사용하는 방식 (Linked List) : 각각의 버킷들을 연결리스트로 만들어 Collision이 ㅂ라생하면 해당 버킷의 list에 추가하는 방식. 연결리스트의 특징을 그대로 이어받아 삭제 or 삽입이 간단함. 하지만 단점도 그대로 물려받아 작은 데이터들을 저장할 때 연결 리스트 자체의 오버헤드에 부담이 됨. 다른 특징으론 버킷을 계속해서 사용하는 Open Address 방식에 비해 테이블의 확장을 늦출 수 있음.
     - Tree를 사용하는 방식(Red-Black Tree) : 기본적인 알고리즘ㅇ느 separate Chaining 방식과 동일하며 연결 리스트 대신 트리를 사용하는 방식.key-value 쌍의 개수를 기준으로 트리를쓸지 정한다. 데이터가 적다면 Linked List.. => 트리는 기본적으로 메모리사용량이 높음. 
3. 데이터가 적다는것은?? => key-value 쌍의 갯수가 6개, 8개를 기준으로 결정..! Linked List와 트리의 기준을 6과 8로 잡은 것은 변경하는데 소요되는 비용을 줄이기 위함임

#### `Open Address` vs `Separate Chaining`

일단 두 방식 모두 Worst Case 는 O(M) 이다. 하지만 연속된 공간에 데이터를 저장하기 때문에 `Separate Chaining`에 비해 캐시 효율이 높다.

따라서 데이터 개수가 충분이 적으면 => Open Address가 성능 더 좋음

`Open Address`는 버킷을 계속해서 사용하기에 `Separate Chaining`방식은 테이블의 확장을 보다 늦출 수 있다.

#### 보조 해시 함수

보조 해시 함수(suppenment hash function)의 목적은 `key`의 해시 값을 변형하여 해시 충돌 가능성을 줄이는 것이다. 주로 `Separate Chaining` 방식을 사용할 때 함께 사용되며 보조 해시 함수로 Worst case에 가까워지는 경우를 줄일수 있음.



#### 해시 버킷 동적 확장(Resize)

해시 버킷의 개수가 적다면 메모리 사용을 아낄 수 있지만 해시 충돌로 인해 성능 상 손실이 발생한다. 그래서 HashMap은 key-value 쌍 데이터 개수가 일정 개수 이상이 되면 해시 버킷의 개수를 두배로 늘림. 이렇게 늘리면 해시 충돌로 인한 성능 손실 문제를 어느정도 해결가능.

해시 버킷 크기를 두 배로 확장하는 임계점은 현재 데이터 개수가 해시 버킷의 개수가 `75%`가 될 때이다. 여기서 0.75 는 load factor라고 불림



#### Reference

- http://d2.naver.com/helloworld/831311
