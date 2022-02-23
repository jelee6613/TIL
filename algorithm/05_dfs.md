# Algorithm_05_dfs



```python
def go(node):
    # 함수의 인자는 시작과 동시에 방문(True) 표시
    went[node] = True

    # 방문한 인자가 갈 수 있는 노드를 순회하며, 만약 방문하지 않았다면 keep going !!
    for going in table[node]:
        if not went[going]:
            go(going)

T = int(input())
for tc in range(1, T+1):
    # node 와 간선의 개수를 input
    nodes, routes = map(int, input().split())

    # node 번호를 인덱스 번호와 맞추기 위해 table 의 인덱스 0 은 깍두기
    table = [[] for _ in range(nodes+1)]

    # 간선의 개수만큼 시작/도착노드 정보를 input 받아서 table 의 해당 노드 리스트에 append
    for _ in range(routes):
        start, end = map(int, input().split())
        table[start].append(end)

    # here 에서 there 까지 갈 수 있니?
    here, there = map(int, input().split())
    # 방문한 노드를 T/F 로 구분하기 위해 False 로 채워진 went 리스트 생성
    went = [False for _ in range(nodes+1)]
    # go 함수에 here 을 넣어서 작동!
    go(here)
    print(f'#{tc} {int(went[there])}')
```



dfs 는 깊이 우선 탐색으로 해당 루트로 갈 수 있는 끝까지 도달한 후, 가장 마지막 갈림길로 돌아와 가지 않았던 곳으로 재진입하여 반복한다.