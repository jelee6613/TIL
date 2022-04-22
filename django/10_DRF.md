# Django_10_DRF



## @api_view

- 기본적으로 GET 메서드만 허용되며 다른 메서드 요청에 대해서는 405 Method Not Allowed
- View 함수가 응답해야 하는 HTTP 메서드의 목록을 리스트 인자로 받음
- DRF에서는 선택이 아닌 **필수적**으로 작성해야 해당 view 함수가 정상 작동



## index [GET]

```python
# urls.py

path('articles/', views.article_list)

# views.py

from django.core import serializers

from rest_framework.response import Response
from rest_framework.decorators import api_view

from .serializers import ArticleSerializer
from .models import Article

@api_view(['GET'])
def article_list(request):
    articles = Article.objects.all()
    serializers = ArticleSerializer(articles, many=True)
    return Response(serializers.data)
```



## detail [GET]

```python
# urls.py

path('articles/<int:article_pk>/', views.article_detail)

# views.py

@api_view(['GET'])
def article_detail(request, article_pk):
    article = get_object_or_404(Article, pk=article_pk)
    serializers = ArticleSerializer(article)
    return Response(serializers.data)
```



## create [POST]

```python
# urls.py

path('articles/', views.article_list)

# views.py

from rest_framework import status

@api_view(['GET', 'POST'])
def article_list(request):
    
    if request.method=="POST":
        serializers = ArticleSerializer(data=request.data)
        if serializers.is_valid(raise_exception=True):
            serializers.save()
            return Response(serializers.data, status=status.HTTP_201_CREATED)
```



### status

- DRF에는 status code를 보다 명확하고 읽기 쉽게 만드는 데 사용할 수 있는 정의된 상수 집합을 제공
- status 모듈에 HTTP status code 집합이 모두 포함되어 있음

`Response(serializer.data, status=201)` 가능하지만, DRF는 권장하지 않음





## delete [DELETE]

```python
# views.py


@api_view(['GET', 'POST', 'DELETE'])
def article_detail(request, article_pk):
    article = get_object_or_404(Article, pk=article_pk)
    if request.method=="DELETE":
        article.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)
```





## update [PUT]

```python
# views. py


@api_view(['GET', 'POST', 'DELETE', 'PUT'])
def article_detail(request, article_pk):
    article = get_object_or_404(Article, pk=article_pk)
    if request.method=="PUT":
        serializers = ArticleSerializer(instance=article, data=request.data)
        if serializers.is_valid(raise_exception=True):
            serializers.save()
            return Response(serializers.data)
```





## create comment [POST]

```python
# urls.py
path('articles/<int:article_pk>/comments', views.comment_create)

# views.py


@api_view(['GET', 'POST'])
def comment_create(request, article_pk):
    article = get_object_or_404(Article, pk=article_pk)
    serializers = CommentSerializer(data=request.data)
    if serializers.is_valid(raise_exception=True):
        serializers.save(article=article)
        return Response(serializers.data)
```



### 문제점

* `serialzers.py`에 작성한 `CommentSerializer`에 `fields = '__all__'` 으로 작성했기 때문에 직렬화 과정에서 `article` 필드가 form-data로 넘겨지지 않아 유효성 검사(is_valid)를 통과하지 못한다. 



### 해결법

- 읽기 전용 필드(read_only_fields) 설정으로 직렬화하지 않고, 반환 값에만 해당 필드가 포함되도록 설정
  검증&저장X / JSON출력 O