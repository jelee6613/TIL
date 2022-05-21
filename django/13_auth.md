# Django_13_Auth



## Authentication & Authorization

- **Authentication** (인증)
  -  자신이라고 주장하는 유저 확인
- **Authorization** (권한/허가)
  - 유저가 자원에 접근할 수 있는지 여부 확인



### Basic Token Authentication

1. Client에서 username, password를 Server에 요청 (POST/login)
2. Server에서 요청 받은 username와 password를 accounts_user테이블에서 찾기
3. authtoken_token테이블에 user와 token 정보 레코드에 추가하고, Client에 응답
4. Client는 브라우저(Local Storage)에 token 정보 저장
5. Client는 Server에 요청을 보낼때마다 Request Header에 토큰 정보를 함께 요청
   Headers - KEY: Authorization, VALUE: Token token정보
   (logout할때도 위의 방법으로 POST 요청하면 authtoken_token테이블에서 삭제되면서 logout)
6. token 정보를 authtoken_token 테이블에서 찾고, 응답



### Authentication (DRF)

1. `$ pip install django-allauth dj-rest-auth` 
   `dj-rest-auth` : signup제외 auth 관련 담당
   `django-allauth` : signup => username, password1, password2(POST/signup) 요청 보내면 Token 정보 응답하고, accounts_user, authtoken_token DB create => signup and login

2. `settings.py`

   ```python
   INSTALLED_APPS = [
       ...
       'rest_framework',
       
       # token 기반의 authentication 사용
       'rest_framework.authtoken',
       
       # signup 제외 auth 관련 담당 (login, logout...)
       'dj_rest_auth',
       
       # django allauth (Registration = signup)
       'django.contrib.sites',
       'allauth',
       'allauth.account',
       'dj_rest.auth.registration',
       ...
   ]
   
   # django.contrib.sites 에서 등록 필요 (django allauth)
   SITE_ID = 1
   
   # drf 설정
   REST_FRAMEWORK = {
       # 기본 인증방식 설정 => (Token)
       'DEFAULT_AUTHENTICATION_CLASSES': [
         'rest_framework.authentication.TokenAuthentication',  
       ],
       
       # 기본 권한 설정
       'DEFAULT_PERMISSION_CLASSES': [
           # 'rest_framework.permissions.AllowAny',  # 인증 유무 상관없이 서비스 이용가능
           'rest_framework.permissions.IsAuthenticated',  # 인증 받아야 서비스 이용가능
       ],
   }
   ```

3. `urls.py`

   ```python
   # urls.py
   
   urlpatterns = [
       path('admin/', admin.site.urls),
       ...
       # 패턴은 자유롭게 설정 가능. 포워딩만 dj_rest_auth 로
       path('api/v1/accounts/', include('dj_rest_auth.urls')),
       path('api/v1/accounts/signup/', include('dj_rest_auth.registration.urls')),
   ]
   ```

   