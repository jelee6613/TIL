# Django_09_REST



## REST

* Representational State Transfer
* API Server를 개발하기 위한 일종의 소프트웨어 설계 방법론
* REST 원리를 따르는 시스템을 RESTful 이란 용어로 지칭



1. 자원 : URI
2. 행위 : HTTP Method
3. 표현 : 자원과 행위를 통해 궁극적으로 표현되는 (추상화된) 결과물, JSON(문자열)



## Response - JsonResponse



* JSON-encoded response를 만드는 HttpResponse의 서브 클래스
* "safe" parameter
  * True (기본값)
  * dict 이외의 객체를 직렬화(Serialization)하려면 False로 설정



```python
# articles/views.py

from django.http import JsonResponse



def article_json_1(request):
  articles = Article2.objects.all()
  articles_json = []

  for article in articles:
    articles_json.append(
      {
        'id': article.pk,
        'title': article.title,
        'content': article.content,
        'created_at': article.created_at,
        'updated_at': article.updated_at,
      }
    )
  return JsonResponse(articles_json, safe=False)
```







## Serialization

* 직렬화
* 데이터 구조나 객체 상태를 동일하거나 다른 컴퓨터 환경에 저장하고, 나중에 재구성할 수 있는 포맷으로 변환하는 과정
* Serializers in Django
  Queryset 및 Model Instance와 같은 복잡한 데이터를 JSON, XML 등의 유형으로 쉽게 변환 할 수 있는 Python 데이터 타입으로 만들어 줌



## Response - Django Serializer

* Django의 내장 HttpResponse를 활용한 JSON 응답 객체
* 주어진 모델 정보를 활용하기 때문에 이전과 달리 필드를 개별적으로 직접 만들 필요가 없음



```python
# articles/views.py

from django.http.response import HttpResponse
from django.core import serializers


def article_json_2(request):
    articles = Article2.objects.all()
    data = serializers.serialize('json', articles)
    return HttpResponse(data, content_type='application/json')
```





## Response - Django REST Framework

### Django REST Framework (DRF)

* Web API 구축을 위한 강력한 Toolkit을 제공하는 라이브러리
  Web API : 웹 애플리케이션 개발에서 다른 서비스에 요청을 보내고 응답을 받기 위해 정의된 명세

* DRF의 Serializer는 Django의 Form 및 ModelForm 클래스와 매우 유사하게 구성되고 작동함

  

### Response

* Django REST framework(DRF) 라이브러리를 사용한 JSON 응답



1.  설치

   ```python
   $ pip install djangorestframework
   
   # settings.py
   
   INSTALLED_APPS = [
       'rest_framework',
   ]
   ```

   

2.  serializers.py 생성

   ```python
   # articles/serializers.py
   
   from rest_framework import serializers
   from .models import Article2
   
   
   class Article2Serializer(serializers.ModelSerializer):
   
     class Meta:
       model = Article2
       fields = '__all__'
   ```

   

3. views.py 작성

   ```python
   # articles/views.py
   
   from rest_framework.decorators import api_view
   from rest_framework.response import Response
   from .serializers import Article2Serializer
   
   
   @api_view()
   def article_json_3(request):
     articles = Article2.objects.all()
     serializer = Article2Serializer(articles, many=True)
     return Response(serializer.data)
   ```

   

