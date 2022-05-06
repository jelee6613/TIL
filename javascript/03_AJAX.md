# JavaScript_03_AJAX



- 페이지를 새로고침 하지 않아도 수행되는 비동기성
- 서버로부터 데이터를 받고 작업 수행



## Threads

- 프로그램이 작업을 완료하기 위해 사용할 수 있는 단일 프로세스
- 각 스레드는 한 번에 하나의 작업만 수행할 수 있음
- JavaScript는 single threaded
  - 즉시 처리하지 못하는 이벤트를 Web API로 보내서 처리
  - 처리된 순서대로 대기실(Task queue)에 줄을 세워 놓고
  - Call Stack이 비면 담당자(Event Loop)가 가장 먼저 온 이벤트를 Call Stack으로 보냄



## Concurrency model

1. Call Stack : 요청이 들어올 때마다 해당 요청을 순차적으로 처리하는 Stack 형태의 자료 구조
2. Web API (Browser API) : JavaScript 엔진이 아닌 브라우저 영역에서 제공하는 API
3. Task Queue : 비동기 처리된 callback 함수가 대기하는 Queue 형태의 자료 구조
4. Event Loop : Call Stack이 비어 있는지 확인하고 비어 있으면 Task Queue에서 대기 중인 callback 함수를 Call Stack으로 push