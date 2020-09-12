## 큐(Queue)

### 큐의 특성

* 스택과 마찬가지로 삽입과 삭제의 위치가 제한적인 자료구조
  * 큐의 뒤에서는 삽입만 하고, 큐의 앞에서는 삭제만 이루어지는 구조
* 선입선출구조(FIFO: First In Fi)
  * 큐에 삽입한 순서대로 원소가 저장되어, 가장 먼저 삽입(First)된 원소는 가장 먼저 삭제(First Out)된다.
* 큐의 주요 연산
  * enQueue(item) - 큐의 뒤쪽(rear 다음)에 원소를 삽입하는 연산
  * deQueue() - 큐의 앞쪽(front)에서 원소를 삭제하고 반환하는 연산
  * createQueue() - 공백 상태의 큐를 생성하는 연산
  * isEmpty() - 큐가 공백상태인지를 확인하는 연산
  * isFull() - 큐가 포화상태인지를 확인하는 연산
  * Qpeek() - 큐의 앞쪽(front)에서 원소를 삭제 없이 반환하는 연산



### BFS(Breadth First Search)

* 너비우선탐색은 탐색 시작점의 인접한 장점들을 먼저 모두 차례로 방문한 후에, 방문했던 정점을 시작점으로 하여 다시 인접한 정점들을 차례로 방문하는 방식
* 인접한 정점들에 대해 탐색을 한 후, 차례로 다시 너비우선탐색을 진행해야하므로, 선입선출 형태의 자료구조인 큐를 활용함.

```python
def BFS(G, v):   					 # 그래프 G, 탐색 시작점 v
    visited = [0]*n       			 # n: 정점의 개수
    queue = []           			 # 큐 생성
    queue.append(v)      			 # 시작점 v를 큐에 삽입
    while queue:         			 # 큐가 비어있지 않은 경우
        t = queue.pop(0) 			 # 큐의 첫 번째 원소 반환
        if not visited[t]:  		 # 방문되지 않은 곳이라면
            visited[t] = True   	 # 방문한 것으로 표시
            visit(t)
        for i in G[t]:          	 # t와 연결된 모든 선에 대해
            if not visited[i]:  	 # 방문되지 않은 곳이라면
                queue.append(i) 	 # 큐에 넣기
```

