## 스택(Stack)1

### 스택의 특성

* 물건을 쌓아 올리듯 자료를 쌓아 올린 형태의 자료구조이다.
* 스택에 저장된 자료는 선형 구조를 갖는다.
  * 선형구조: 자료 간의 관계가 1대1의 관계를 갖는다.
  * 비선형구조: 자료 간의 관계가 1대N의 관계를 갖는다.
* 스택에 자료를 삽입하거나 스택에서 자료를 꺼낼 수 있다.
* 마지막에 삽입한 자료를 가장 먼저 꺼낸다. 후입선출(LIFO, Last-In-First-Out)이라고 부른다.

#### 연산

* 삽입: 저장소에 자료를 저장한다. 보통 push라고 부른다.
* 삭제: 저장소에 자료를 꺼낸다. 꺼낸 자료는 삽입한 자료의 역순으로 꺼낸다. 보통 pop이라고 부른다.
* 스택이 공백인지 아닌지를 확인하는 연산. isEmpty
* 스택의 top에 있는 item을 반환하는 연산. peek



#### 스택의 push 알고리즘

```python
# Append 메소드를 통해 리스트의 마지막에 데이터를 삽입

def push(item):
    s.append(item)
```



#### 스택의 pop 알고리즘

```python
def pop():
    if len(s) == 0:
        #underflow
        return
    else:
        return s.pop(-1)
```



#### 스택 구현

```python
stack = []
def push(item):
    stack.append(item)

def pop():
    if len(stack) == 0:
        print("Stack is empty")
        return
    else:
        return stack.pop()

push(1)
push(2)
push(3)
print(pop())
print(pop())
print(pop())
```



#### 스택 응용1: 괄호검사

* 괄호의 종류: 대괄호('[', ']'), 중괄호('{', '}'), 소괄호('(', ')')
* 조건
  * 왼쪽 괄호의 개수와 오른쪽 괄호의 개수가 같아야 한다.
  * 같은 괄호에서 왼쪽 괄호는 오른쪽 괄호보다 먼저 나와야 한다.
  * 괄호 사이에는 포함 관계만 존재한다.
* 문자열에 있는 괄호를 차례대로 조사하면서 왼쪽 괄호를 만나면 스택에 삽입하고, 오른쪽 괄호를 만나면 스택에서 top 괄호를 삭제한 후 오른쪽 괄호와 짝이 맞는지를 검사한다.

```python
check_bracket(target):
    # 여는 괄호가 나오면 stack에 push
    # 닫는 괄호가 나오면 stack에 pop
    # 문장이 끝났을 때, stack이 비어있으면 정상적인 괄호
    # 아니라면 비정상 괄호

    stack = list()
    for i in range(len(target)):
        # 문자가 여는 괄호라면 push
        # 닫는 괄호면 pop, pop했는데 비어있으면 False
        if target[i] == '(' or target[i] == '[' or target[i] == '{':
            stack.append(target[i])   # 여는 괄호가 잇으면 push
        elif target[i] == ')' or target[i] == ']' or target[i] == '}':
            if len(stack) == 0:     # 닫는 괄호가 나왔는데 비어있으면
                return False
            tmp = stack.pop()             # 비어있지 않으면 pop하고, 짝이 맞는지 검사 해야한다.
            if target[i] == ')' and tmp == '(':
                continue
            elif target[i] == ']' and tmp == '[':
                continue
            elif target[i] == '}' and tmp == '{':
                continue
            ########### 여기까지 진입하면 무슨의미??########
            # 스택은 비어있지 않은데, 짝이 맞지 않음
            return False

    # 반복문이 끝났을 때, stack이 비어있으면 True
    # 아니면 False
    if len(stack) != 0:
        return False
    else:
        return True

str = "({})[()()]"
result = check_bracket(str)
print(result)
```



#### 스택 응용2: Function call

* 프로그램에서의 함수 호출과 복귀에 따른 수행 순서를 관리
  * 가장 마지막에 호출된 함수가 가장 먼저 실행을 완료하고 복귀하는 후입선출 구조이므로, 후입선출 구조의 스택을 이용하여 수행순서 관리
  * 함수 호출이 발생하면 호출한 함수 수행에 필요한 지역변수, 매개변수 및 수행 후 복귀할 주소 등의 정보를 스택 프레임(stack frame)에 저장하여 시스템 스택에 삽입
  * 함수의 실행이 끝나면 시스템 스택의 top원소(스택 프레임)를 삭제(pop)하면서 프레임에 저장되어 있던 복귀주소를 확인하고 복귀
  * 함수 호출과 복귀에 따라 이 과정을 반복하여 전체 프로그램 수행이 종료되면 시스템 스택은 공백 스택이다.

![function call](19_%EC%8A%A4%ED%83%9D(Stack)1.assets/function%20call.PNG)



#### 재귀호출

* 자기 자신을 호출하여 순환 수행되는 것
* 함수에서 실행해야 하는 작업의 특성에 따라 일반적인 호출방식보다 재귀호출방식을 사용하여 함수를 만들면 프로그램의 크기를 줄이고 간다하게 작성

```python
# 재귀호출의 예) factorial
n! = n * (n-1)!
(n-1)! = (n-1) * (n-2)!
(n-2)! = (n-2) * (n-3)!
....
2! = 2 * 1!
1! = 1
# 마지막에 구한 하위 값을 이용하여 상위 값을 구하는 작업을 반복
```

* 피보나치 수를 구하는 재귀함수

```python
# 0과 1로 시작하고 이전의 두 수 합을 다음 항으로 하는 수열을 피보나치라 한다.
def fibo(n):
    if n < 2:
        return n
    else:
        return fibo(n-1) + fibo(n-2)
```



#### Memoization(메모이제이션)

* 메모이제이션은 컴퓨터 프로그램을 실행할 때 이전에 계산한 값을 메모리에 저장해서 매번 다시 계산하지 않도록 하여 전체적인 실행속도를 빠르게 하는 기술이다. 
* 동적 계획법의 핵심이 되는 기술
* Memoization 방법을 적용한 알고리즘

```python
# memo를 위한 배열을 할당하고, 모두 0으로 초기화 한다.
# memo[0]을 0으로 memo[1]는 1로 초기화 한다.

def fibo1(n):
    global memo
    if n >= 2 and len(memo) <= n:
        memo.append(fibo1(n-1) + fibo1(n-2))
    return memo[n]

memo = [0, 1]
```



#### DP(Dynamic Programming)

* 동적 계획 알고리즘은 그리디 알고리즘과 같이 최적화 문제를 해결하는 알고리즘이다.
* 동적 계획 알고리즘은 먼저 입력 크기가 작은 부분 문제들을 모두 해결한 후에 그 해들을 이용하여 보다 큰 크기의 부분 문제들을 해결하여, 최종적으로 원래 주어진 입력의 문제를 해결하는 알고리즘이다.
* 피보나치 수 DP 적용 알고리즘

```python
def fibo2(n):
    f = [0, 1]
    for i in range(2, n+1):
        f.append(f[i-1] + f[i-2])
        
    return f[n]
```

* DP의 구현 방식
  * recursive 방식: fib1()
  * iterative 방식: fib2()
  * memoization을 재귀적 구조에 사용하는 것보다 반복적 구조로 DP를 구현한 것이 성능면에서 보다 효율적이다.
  * 재귀적 구조는 내부에 시스템 호출 스택을 사용하는 오버헤드가 발생하기 때문이다.



#### DFS(깊이우선탐색)

* 비선형구조인 그래프 구조는 그래프로 표현된 모든 자료를 빠짐없이 검색하는 것이 중요함.
* 두 가지 방법
  * 깊이 우선 탐색(Depth First Search, DFS)
  * 너비 우선 탐색(Breadth First Search, BFS)
* 시작 장점의 한 방향으로 갈 수 있는 경로가 있는 곳까지 깊이 탐색해 가다가 더 이상 갈 곳이 없게 되면, 가장 마지막에 만났던 갈림길 간선이 있는 정점으로 되돌아와서 다른 방향의 정점으로 탐색을 계속 반복하여 결국 모든 정점을 방문하여 순회방법
* 가장 마지막에 만났던 갈림길의 정점으로 되돌아가서 다시 깊이 우선 탐색을 반복해야 하므로 후입선출 구조의 스택 사용

#### DFS 알고리즘

* 시작 정점 v를 결정하여 방문한다.
* 정점 v에 인접한 정점 중에서
  * 방문하지 않은 정점 w가 있으면, 정점 v를 스택에 push하고 정점 w를 방문한다. 그리고 w를 v로 하여 다시 반복한다.
  * 방문하지 않은 장점이 없으면, 탐색의 방향을 바꾸기 위해서 스택을 pop하여 받은 가장 마지막 방문 정점을 v로 하여 다시 반복한다.
* 스택이 공백이 될 때 까지 이전 과정을 반복한다.

```python
visited[], stack[] 초기화
DFS(v)
	v 방문;
    visited[v] <- true;
    do {
        if (v의 인접 정점 중 방문 안한 w 찾기)
        	push(v);
        while(w) {
            w 방문;
            visited[w] <- true;
            push(w);
            v <- w;
            v의 인접 정점 중 방문 안한 w 찾기
        }
        v <- pop(stack);
    } while(v)
end DFS()
```

