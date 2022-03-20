# Algorithm_08_BFS



## BFS

너비우선탐색

한 단계씩 발전 => 최단거리, 영역/조건 탐색



### 기본 구조

1. queue, visited 등 초기화

2. queue에 초기 데이터(들) 삽입 / visited 배열 표시 및 필요작업

3. 큐에 데이터 있는 동안 반복 while

4. queue에서 데이터 1개 꺼냄

5. 4/8방향, 연결된 경우 등 '조건'에 맞으면 큐 삽입, next 좌표/노드 계산해서 범위내 '조건' 맞으면 queue에 next 삽입, visited체크 및 필요작업

   