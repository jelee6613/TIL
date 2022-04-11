# Django_05_HTTP



## Error

* 1xx : 정보 제공 관련 응답
* 2xx : 성공적인 응답
* 3xx : 리다이렉트 관련
* 4xx : 클라이언트 에러
* 5xx : 서버 에러



## Allowed HTTP methods

요청 메서드에 따라 view 함수 실행

Django View decorators

* require_http_methods()

  view 함수가 특정 method 요청에만 실행함

```python
@require_http_methods(["GET", "POST"])
def 함수(request):
    blah~blah
```



* require_POST()
  view 함수가 POST method 요청만 실행

```python
@require_POST
def delete(request, pk):
    blah~blah
```



* require_safe()
  view 함수가 GET만 허용
  django는 require_GET 대신 require_safe 사용을 권장

```python
@require_safe
def index(request):
    blah blah
```



## django.views.decorators.http

```python
# views.py

from django.views.decorators.http import require_POST, require_http_methods, require_safe

@require_safe
def index(request):
  students = Student.objects.all()
  context = {
    'students': students,
  }
  return render(request, 'classroom/index.html', context)

# POST와 GET만 받음
@require_http_methods(["POST", "GET"])
def create(request):
  if request.method == "POST":
    form = StudentForm(request.POST)
    if form.is_valid():
      student = form.save()
      return redirect('classroom:detail', student.pk)
  
  else:
    form = StudentForm()
  context = {
    'form': form,
  }
  return render(request, 'classroom/create.html', context)

# POST만 받음
@require_POST
def delete(request, pk):
  student = get_object_or_404(Student, pk=pk)
  student.delete()
  return redirect('classroom:index')
```



### get_object_or_404

* get_object_or_404()
  해당 객체가 없으면 DoesNotExist 예외 대신 Http 404를 raise
  상황에 따라 적절한 예외처리, 클라이언트에게 올바른 에러 상황을 전달하는 것 또한 중요한 개발 과정

```python
article = get_object_or_404(모델이름, pk=pk)
```





## 이미지

이미지필드를 사용하기 위한 단계

$ pip install Pillow



1. settings.py에 MEDIA_ROOT, MEDIA_URL 설정
   MEDIA_ROOT : 사용자가 업로드 한 파일을 보관할 디렉토리의 절대 경로
   django는 성능을 위해 업로드 파일을 데이터베이스에 저장 X, 파일의 경로만 저장

   ```python
   # settings.py
   
   MEDIA_ROOT = BASE_DIR/'media'
   ```

   MEDIA_URL : MEDIA_ROOT에서 제공되는 미디어를 처리하는 URL

   업로드 된 파일의 주소를 만들어 주는 역할

   ```python
   # settings.py
   
   MEDIA_URL = '/media/'
   ```

   

2. upload_to 속성으로 업로드 된 파일에 사용 할 MEDIA_ROOT의 하위 경로 지정

3. 업로드 된 파일의 경로는 django가 제공하는 url 속성을 사용

```html
<img src="{{ article.image.url }}" alt="{{ article.image }}">
```





```python
class Article(models.Model):
    image = models.ImageField(upload_to='images/', blank=True)
```

* blank = True : 이미지 필드에 빈 문자열이 허용되도록 설정 (이미지 업로드가 강제가 아닌 선택할 수 있도록)
* upload_to : 실제 이미지가 저장되는 경로 지정



### enctype

* input 타입이 file일때 아래 enctype 필요

```html
<form method="POST" enctype="multipart/form-data">
    {% csrf_token %}
    {{ form.as_p }}
    <button>
        작성
    </button>
</form>
```



### 이미지가 없는 경우에도 detail 출력

```html
# detail.html

{% if article.image %}
	<img src="{{ article.image.url }}" alt="{{ article.image }}"
{% endif %}
```



### 이미지 리사이징

* Install Pillow
* pip install django-imagekit
* Add 'imagekit' to your INSTALLED_APPS list in your project's settings.py

```python
# models.py

from django.db import models
from imagekit.models import ProcessedImageField
from imagekit.processors import ResizeToFill

class Article(models.Model):
  # image = models.ImageField(upload_to='images/', blank=True)
  thumbnail = ProcessedImageField(upload_to='thumbnails/',
                                  processors=[ResizeToFill(100, 50)],
                                  format='JPEG',
                                  blank=True,
                                  options={'quality: 60'})
```



* 기존 ImageField는 원본 저장 관련인데, db에 무리가 갈 수 있으므로 주석처리하고 ProcessedImageField로 이미지 파일 리사이징해서 관리
* ResizeToFill 대신 Thumbnail ?





### 사용자가 업로드 한 파일 제공하기

```python
# project/urls.py

from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    path('admin/', admin.site.urls),
    path('articles/', include('articles.urls')),
    path('classroom/', include('classroom.urls')),
    path('accounts/', include('accounts.urls')),
] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)

```

