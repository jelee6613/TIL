# Django_07_ForeignKey



## Foreign Key

* 외래키는 제약사항이다.



## on_delete

* 외래키가 참조하는 객체가 사라졌을 때 외래키를 가진 객체를 어떻게 처리할 지를 정의
  * CASCADE : 부모 객체가 삭제 됐을 때 이를 참조하는 객체도 삭제
  * SET_NULL
  * SET_DEFAULT
  * SET()
  * DO_NOTHING
  * RESTRICT
* 데이터 무결성 중요

abcd로 생성하면 abcd_id로 생성되며, 소문자 권장



## 역참조

Article(1) => Comment(N)

`article.comment` X, `article.comment_set` O

Article 클래스에는 Comment와의 어떠한 관계도 작성되어 있지 않음



## 참조

Comment(N) => Article(1)

댓글의 경우 어떠한 댓글이든 반드시 자신이 참조하고 있는 게시글이 있으므로 `comment.article` 접근 가능



## save(commit=False)

아직 데이터베이스에 저장되지 않은 인스턴스를 반환

저장하기 전에 객체에 대한 사용자 지정 처리 수행



## Setting

1. App (accounts, articles) 생성

2. ```python
   # accounts/models.py
   
   from django.contrib.auth.models import AbstractUser
   
   class User(AbstractUser):
       pass
   ```

3. ```python
   # settings.py
   
   AUTH_USER_MODEL = 'accounts.User'
   ```

4. ```python
   # articles/models.py
   
   from django.conf import settings
   
   # N 클래스에 참조할 모델을 작성하되, User는 아래와 같이 작성
   models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=blah blah)
   
   # User가 아닌 경우,
   models.ForeignKey(참조클래스, on_delete=blah blah)
   
   
   ## 위와 같은 경우 제외하고는 아래와 같은 방법으로 user 사용
   from django.contrib.auth import get_user_model
   
   User = get_user_model()
   ```

5.  CustomUserCreationForm

   ```python
   # accounts/forms.py
   
   from django.contrib.auth.forms import UserCreationForm 
   from  django.contrib.auth import get_user_model
   
   User = get_user_model()
   
   class CustomUserCreationForm(UserCreationForm):
       
   	class Meta:
           model = User
           fields = UserCreationForm.Meta.fields
   ```

6. Login

   ```python
   def login(request):
       if request.method == "POST":
           form = AuthenticationForm(request, request.POST)
           if form.is_valid():
               user = form.get_user()
               auth_login(request, user)
               return redirect('articles/article_index')
       
       else:
           form = AuthenticationForm()
       context = {
           'form': form,
       }
       return render(request, 'accounts/login.html', context)
   ```

   

## DB 지우기

* rm db.sqlite3
* rm app이름/migrations/0*