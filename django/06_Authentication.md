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

* 사용자가 로그인되어 있지 않으면, settings.LOGIN_URL에 설정된 문자열 기반 절대 경로로 redirect
  LOGIN_URL의 기본 값은 '/accounts/login/'

* 사용자가 로그인되어 있으면 정상적으로 view 함수 실행

* 인증 성공 시 사용자가 redirect 되어야하는 경로는 "next"라는 쿼리 문자열 매개 변수에 저장됨
  /accounts/login/?next=/articles/create/

  * 로그인이 정상적으로 진행되면 기존에 요청했던 주소로 redirect 하기 위해 마치 주소를 keep 해주는 것

  * 단, 별도로 처리 해주지 않으면 우리가 view에 설정한 redirect 경로로 이동하게 됨

    ```python
    # accounts/views.py
    
    def login(request):
        if request.user.is_authenticated:
            return redirect('articles:index')
        
        if request.method == "POST":
            form = AuthenticationForm(request, reuqest.POST)
            if form.is_valid():
                auth_login(request, form.get_user())
                return redirect(request.GET.get('next') or 'articles:index')
        
        else:
            form = AuthenticationForm()
        context = {
            'form': form,
        }
        return render(request, 'accounts/login.html', context)
    ```

  

## 회원가입

```python
# accounts/views.py

def signup(request):
    if reuqest.method == "POST":
        form = UserCreationForm(request.POST)
        if form.is_valid():
            user = form.save()
            auth_login(request, user)  # 회원가입 후 자동 로그인
            return redirect('articles:index')
    else:
        form = UserCreationForm()
    context = {
        'form': form,
    }
    return render(request, 'accounts/signup.html', context)
```





## 회원탈퇴

* 회원탈퇴는 DB에서 사용자를 삭제하는 것과 같음



```python
# accounts/views.py

def delete(reuqest):
    if request.user.is_authenticated:
        request.user.delete()
        auth_logout(request)  # 세션도 함께 지운다.
    return redirect('articles:index')
```





## 회원정보 수정

* `UserChangeForm` : 사용자의 정보 및 권한을 변경하기 위해 admin 인터페이스에서 사용되는 ModelForm



```python
# accounts/views.py

def update(request):
    if request.method == "POST":
        form = UserChangeForm(requset.POST, instance=request.user)
        if form.is_valid():
            form.save()
            return redirect('articles:index')
    else:
        form = UserchangeForm(instance=request.user)
    context = {
        'form': form,
    }
    return render(request, 'accounts/update.html', context)
```





* `CustomUserChangeForm`

```python
# accounts/forms.py

from django.contrib.auth.forms import UserChangeForm
from django.contrib.auth import get_user_model

class CustomUserChangeForm(UserChangeForm):
    
    class Meta:
        model = get_user_model()
        fields = ('email', 'first_name', 'last_name',)  # 수정시 필요한 필드만 작성
```



```python
# accounts/views.py

def update(request):
    if request.method == "POST":
        form = CustomUserChangeForm(request.POST, instance=request.user)
        if form.is_valid():
            form.save()
            return redirect('articles:index')
    else:
        form = CustomUserChangeForm(instance=request.user)
    context = {
        'form': form,
    }
    return render(request, 'accounts/update.html', context)
```

