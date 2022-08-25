## 1. 가장 기본이 되는 자료구조: 스택과 큐

- 스택(Stack)
  - 선입후출
  - 입구와 출구가 동일 -> 박스 쌓기, 또는 프링글스 통
  - 리스트 자료형을 이용 (오른쪽이 입출구)
  - stack = []
  - append(), pop() 메서드 이용
  - print(stack[::-1]) <- 스택의 최상단 원소부터 출력
  - print(stack) <- 스택의 최하단 원소부터 출력

- 큐(Queue)
  - 선입선출
  - 오른쪽이 입구, 왼쪽이 출구 -> 입구와 출구가 모두 뚫려있는 터널 형태, 대기열
  - deque 라이브러리를 이용 (list 자료형은 시간복잡도가 더 높아서 비효율적으로 동작)
  - queue = deque()
  - append(), popleft() 메서드 이용
  - print(queue) <- 먼저 들어온 순서대로 출력
  - queue.reverse()
  - print(queue) <- 나중에 들어온 원소부터 출력

---



















---

## 5. 간단하면서 기본적인 정렬 알고리즘: 선택 정렬과 삽입 정렬

- 선택 정렬
  - 처리되지 않은 데이터 중에서 가장 작은 데이터를 선택해 맨 앞에 있는 데이터와 바꾸는 것을 반복
  - 시간 복잡도는 O(N<sup>2</sup>) = N + (N-1) + (N-2) + ... + 2
- 삽입 정렬
  - 처리되지 않은 데이터를 하나씩 골라 적절한 위치에 삽입. 선택 정렬에 비해 구현 난이도가 높지만 더 효율적으로 동작
  - 선택 정렬과 마찬가지로 반복문이 두 번 중첩되어 사용되므로 시간 복잡도는 O(N<sup>2</sup>)이다. 그러나 삽입 정렬은 현재 리스트의 데이터가 거의 정렬되어 있는 상태라면 매우 빠르게 동작하여, 최선의 경우 O(N)의 시간 복잡도를 가질 수 있다.

---

## 6. 더 빠른 정렬 알고리즘: 퀵 정렬과 계수 정렬

- 퀵 정렬

  - 기준 데이터를 설정하고 그 기준보다 큰 데이터와 작은 데이터의 위치를 바꾸는 방법. 일반적인 상황에서 가장 많이 사용되며, 병합 정렬과 더불어 대부분의 프로그래밍 언어의 표준 정렬 라이브러리의 근간이 되는 알고리즘.

  - 가장 기본적인 퀵 정렬은 첫 번째 데이터를 기준 데이터(pivot)로 설정한다.

  - 알고리즘

    0. 배열의 첫 번째 데이터를 pivot으로 설정한다.

    1. 왼쪽에서부터 pivot보다 큰 데이터를 선택하고 오른쪽에서부터 pivot보다 작은 데이터를 선택해서 두 데이터의 위치를 서로 변경한다.
    2. 1을 반복한다.
    3. 두 데이터를 선택했을 때 위치가 엇갈리는 경우 pivot과 '작은 데이터'의 위치를 서로 변경한다.
    4. [분할 완료] 이제 pivot의 왼쪽에 있는 데이터는 모두 pivot보다 작고, pivot의 오른쪽에 있는 데이터는 모두 pivot보다 크다. 이렇게 pivot을 기준으로 데이터 묶음을 나누는 작업을 분할(divide)이라고 한다.
    5. 왼쪽 데이터 묶음에 대해 0~4의 퀵 정렬을 수행하고, 오른쪽 데이터 묶음에 대해 또 0~4의 퀵 정렬을 수행한다. 이렇듯 퀵 정렬은 재귀적으로 수행되고, 수행될 때마다 정렬 범위가 점점 좁아진다.

  - 이상적인 경우 분할이 절반씩 일어난다면 전체 연산 횟수로 O(NlogN)을 기대할 수 있다. 따라서 평균의 경우 시간 복잡도로 O(NlogN)을 갖지만, 최악의 경우 O(N<sup>2</sup>)을 갖는다. pivot 값 설정에 따라 분할이 절반에 가깝게 이뤄지지 않고 한 쪽 방향으로 편향된 분할이 발생할 수 있기 때문이다. 표준 라이브러리의 경우에는 항상 O(NlogN)을 보장한다.

- 계수 정렬
  - 특정한 조건이 부합할 때만 사용할 수 있지만 매우 빠르게 동작하는 정렬 알고리즘
  - 데이터의 크기 범위가 제한되어 정수 형태로 표현할 수 있을 때 사용 가능
  - 데이터의 개수가 N, 데이터(양수) 중 최댓값이 K일 때 최악의 경우에도 수행 시간 O(N+K)를 보장
  - 시간 복잡도와 공간 복잡도는 모두 O(N+K)
  - 때에 따라 심각한 비효율성을 초래할 수 있음. ex) 데이터가 0과 999,999 단 두 개만 존재하는 경우
  - 동일한 값을 갖는 데이터가 여러 개 등장할 때 효과적으로 사용할 수 있음. ex) 성적

---













---

## 8. 그래프 탐색의 기본, DFS와 BFS

- DFS(Depth-First Search)
  - 깊이 우선 탐색
  - 스택 자료구조 혹은 재귀 함수를 이용
  - 알고리즘
    1. 탐색 시작 노드를 스택에 삽입하고 방문 처리를 한다.
    2. 스택의 최상단 노드에 방문하지 않은 인접한 노드가 하나라도 있으면 그 노드를 스택에 넣고 방문 처리한다. 방문하지 않은 인접 노드가 없으면 스택에서 최상단 노드를 꺼낸다.
    3. 더이상 2번의 과정을 수행할 수 없을 때까지 반복한다.
  - 각 노드가 연결된 정보를 2차원 리스트로 표현
  - 각 노드가 방문된 정보를 1차원 리스트로 표현
  - 노드의 개수가 n개면 원소가 (n+1)개인 리스트 객체를 만들어 주고 0 인덱스는 사용하지 않는다.

- BFS(Breadth-First Search)
  - 너비 우선 탐색
  - 큐 자료구조를 이용
  - 알고리즘
    1. 탐색 시작 노드를 큐에 삽입하고 방문 처리를 한다.
    2. 큐에서 노드를 꺼낸 뒤에 해당 노드의 인접 노드 중에서 방문하지 않은 노드를 모두 큐에 삽입하고 방문 처리한다.
    3. 더이상 2번의 과정을 수행할 수 없을 때까지 반복한다.
  - 각 노드가 연결된 정보를 2차원 리스트로 표현
  - 각 노드가 방문된 정보를 1차원 리스트로 표현
  - 노드의 개수가 n개면 원소가 (n+1)개인 리스트 객체를 만들어 주고 0 인덱스는 사용하지 않는다.
  - 간선의 비용이 모두 같을 때 최단거리를 탐색하기 위해 사용할 수 있는 알고리즘

---









---

## 17. 프로그래밍의 꽃: 재귀 함수

- 재귀 함수(Recursive Function)
  - 자기 자신을 다시 호출하는 함수
  - 재귀 함수의 종료 조건을 반드시 명시해야 함. 그러지 않으면 함수가 무한히 호출됨.
  - 재귀 함수를 이용하면 마치 스택에 데이터를 넣었다 꺼내는 것과 마찬가지로, 각각의 함수에 대한 정보가 실제로 스택 프레임에 담겨서 차례대로 호출되었다가 가장 마지막에 호출된 함수부터 차례대로 종료됨.
  - 모든 재귀 함수는 반복문을 이용하여 동일한 기능을 구현할 수 있는데, 재귀 함수가 반복문보다 유리한 경우도 있고 불리한 경우도 있으므로, 특정 문제를 만났을 때 더 좋은 방법을 고려하여 문제를 풀어야 한다.
  - 컴퓨터가 함수를 재귀적으로 호출하면 실제로는 컴퓨터 메모리 내부의 스택 프레임에 차곡차곡 쌓인다. 그래서 스택을 사용해야 할 때 구현상 스택 자료구조를 사용하지 않고 그냥 재귀 함수를 이용하는 경우가 많다. DFS를 간결한 코드로 작성하기 위해 단순히 재귀 함수를 이용해서 DFS를 구현하곤 한다.

---











---

## 21. 동적 계획법: 메모리를 더 소모하여 속도를 비약적으로 향상시키는 기법

- 다이나믹 프로그래밍의 사용 조건
  1. 최적 부분 구조: 큰 문제를 작은 문제로 나눌 수 있다.
  2. 중복되는 부분 문제: 동일한 작은 문제를 반복적으로 해결한다.

- 구현 방식

  - 하향식(탑다운) - 메모이제이션(Memoization)

    : 한 번 계산한 결과를 메모리 공간에 메모하는 기법으로, 같은 문제를 다시 호출하면 메모했던 결과를 그대로 가져온다. 값을 기록해 놓는다는 점에서 캐싱(Caching)이라고도 한다. 구현 시 재귀함수 사용.

  - 상향식(보텀업)

    : 다이나믹 프로그래밍의 전형적인 형태. 결과 저장용 리스트/배열은 DP 테이블이라고 부른다. 구현 시 반복문 사용.

- 다이나믹 프로그래밍 문제에 접근하는 방법

  - 주어진 문제가 다이나믹 프로그래밍 유형임을 파악하는 것이 중요하다.
  - 가장 먼저 그리디, 구현, 완전탐색 등의 아이디어로 문제를 해결할 수 있는지 검토한다. 다른 알고리즘으로 풀이 방법이 떠오르지 않으면(너무 많은 시간 복잡도가 소요된다고 판단되면) 다이나믹 프로그래밍을 고려한다.
  - 일단 재귀함수로 비효율적인 완전탐색 프로그램을 작성한 뒤(탑다운), 작은 문제에서 구한 답이 큰 문제에서 그대로 사용될 수 있으면 코드를 개선하는 방법을 사용할 수 있다.
  - 일반적인 코딩 테스트 수준에서는 기본 유형의 다이나믹 프로그래밍 문제가 출제되는 경우가 많다.

---




