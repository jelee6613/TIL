

# Django_12_CORS



- Server (정보 제공)
  클라이언트에게 '정보', '서비스'를 제공하는 컴퓨터 시스템
  DB와 통신하며 데이터 CRUD
- Client (정보 요청&표현)
  서버가 제공하는 **서비스를 요청**하고, 서비스 요청에 필요한 인자를 **서버가 요구하는 방식에 맞게 제공**하며, 서버의 응답을 **사용자에게 적절한 방식으로 표현**하는 기능을 가진 시스템



Same-origin policy (SOP)

Same origin http(Protocol) :// localhost(Host) : 3000(Port) / posts/3(Path)
두 URL의 Protocol, Port, Host가 모두 같아야 동일한 출처라 할 수 있음

- 동일 출처 정책
- 특정 출처(origin)에서 불러온 문서나 스크립트가 다른 출처에서 가져온 리소스와 상호작용 하는 것을 제한하는 보안 방식
- 잠재적으로 해로울 수 있는 문서를 분리함으로써 공격받을 수 있는 경로를 줄임



Cross-Origin Resource Sharing (CORS)

- 교차 출처 리소스(자원) 공유
- 추가 HTTP header를 사용하여 특정 출처에서 실행중인 웹 애플리케이션이 다른 출처의 자원에 접근 할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제
- 다른 출처의 리소스를 불러오려면 그 출처에서 올바른 CORS header를 포함한 응답을 반환해야 함



Why CORS ?

1. 브라우저 & 웹 애플리케이션 보호
   - 악의적인 사이트의 데이터 가져오지 않도록 사전 차단
   - 응답으로 받는 자원에 대한 최소한의 검증
   - 서버는 정상적으로 응답하지만 브라우저에서 차단
2. Server의 자원 관리
   - 누가 해당 리소스에 접근 할 수 있는지 관리 가능



CORS 시나리오 예시

1. Vue.js에서 A 서버로 요청
2. A 서버는 Access-Control-Allow-Origin에 특정한 origin을 포함 시켜 응답
   - 서버는 CORS Policy와 직접적인 연관이 없고 그저 요청에 응답함
3. 브라우저는 응답에서 Access-Control-Allow-Origin을 확인 후 허용 여부를 결정
4. 프레임워크 별로 이를 지원하는 라이브러리가 존재
   - django는 django-cors-headers 라이브러리를 통해 응답 헤더 및 추가 설정 가능



Start

1. `$ pip install django-cors-headers`

2. settings.py 추가

   ```python
   # settings.py
   
   INSTALLED_APPS = [
       ...
       'corsheaders',
       ...
   ]
   
   MIDDLEWARE = [
       ...
       'corsheaders.middleware.CorsMiddleware',
       'django.middleware.common.CommonMiddleware',
       ...
   ]
   
   # 특정 origin 에게만 교차 출처 허용
   """
   CORS_ALLOWED_ORIGINS = [
       # Vue LocalHost
       'http://localhost:8080',
       'http://127.0.0.1:8001',
   	]
   """
   
   # 모두에게 교차 출처 허용
   CORS_ALLOW_ALL_ORIGINS = True
   ```

   

   