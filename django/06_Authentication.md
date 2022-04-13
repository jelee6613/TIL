# Django_06_Authentication



```python
#settings.py/INSTALLED_APPS

django.contrib.auth  	     # 인증 프레임워크의 핵심과 기본 모델을 포함
django.contrib.contenttypes  # 사용자가 생성한 모델과 권한을 연결할 수 있음
```





## startapp accounts

* 앱 이름이 반드시 accounts일 필요는 없으나, auth 관련해 Django 내부적으로 accounts라는 이름으로 사용되기 때문에 accounts 권장

1. ```bash
   $ python manage.py startapp accounts
   ```

2. app 등록 및 url 설정



## 로그인

* session을 Create하는 로직
* 인증에 관한 `AuthenticationForm` 이용
* login(request, user, backend=None)



```python
# accounts/views.py
from django.contrib.auth.forms import AuthenticationForm
from django.contrib.auth import login as auth_login  # 함수 이름과 겹치므로 수정

def login(request):
    if request.method == "POST":
        form = AuthenticationForm(request, request.POST)
        if form.is_valid():
            auth_login(request, form.get_user())
            return redirect('articles:index')
    else:
        form = AuthenticationForm()
    context = {
        'form': form,
    }
    return render(request, 'accounts/login.html', context)
```





## 로그아웃

* session을 Delete하는 로직
* logout(request)
* DB에서 session data를 완전히 삭제하고, 클라이언트의 쿠키에서도 session id가 삭제됨
* 다른 사람이 동일한 웹 브라우저를 사용해 이전 사용자 세션 데이터에 접근하는 것을 방지



```python
# accounts/views.py
from django.views.decorators.http import require_POST
from django.contrib.auth import logout as auth_logout

@require_POST
def logout(request):
    auth_logout(request)
    return redirect('articles:index')
```



## 로그인 사용자에 대한 액세스

### is_authenticated (attribute)



인증된 사용자라면 로그아웃 버튼, 아니라면 로그인 버튼 표시

```html
<!-- template -->

{% if request.user.is_authenticated %}
<h3>Hello, {{ user }}</h3>
<form action="{% url 'accounts:logout' %}" method="POST">
    {% csrf_token %}
    <input type="submit" value="Logout">
</form>
{% else %}
<a href="{% url 'accounts:login' %}">Login</a>
{% endif %}
```



```python
# accounts/views.py

# 인증된 사용자라면 로그인 로직 수행 X
def login(requset):
    if request.user.is_athenticated:
        return redirect('articles:index')

# 인증된 사용자만 로그아웃 로직 수행
def logout(request):
    if request.user.is_athenticated:
        auth_logout(request)
    return redirect('articles:index')
```



### login_required (decorator)