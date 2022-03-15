

# Django_03_Model



## 시작하기에 앞서

```bash
$ python -m venv venv
$ source venv/Script/activate
$ pip install django==3.2.12
$ pip install django_extensions  # App 등록, 복수형 권장
$ pip install ipython
$ django-admin startproject [Project 이름] .
$ python manage.py startapp [App 이름]  # App 등록, 복수형 권장
```





## pip install

`$ pip install django_extensions`		*# 3rd app => settings.py 등록*

`$ pip install ipython`



## models.py

### Table 생성/수정 반영 (Migration)

1)

```python
# 테이블 생성
class Articles(models.Model):

	# 인스턴스 생성(열)
    title = models.CharField(max_length=20)
    content = models.TextField()
	create_at = models.DateTimeField(auto_now_add=True)
	update_at = models.DateTimeField(auto_now=True)
    
    # 이쁘게 보여주기
    def __str__(self):
        return f'{self.title}: {self.content}'
```



2)

```bash
$ python manage.py makemigrations [App 이름]
$ python manage.py migrate [App 이름]
```



* 중간에 인스턴스 추가할 땐 인자에 `default=값` 주고, 2) 반복
* migrations 파일은 DB 스키마를 위한 시스템



## Data CRUD



* 데이터베이스는 CRUD 하기 위한 것



```bash
$ python manage.py shell_plus --print-sql  # ipython 설치해서 주피터처럼 보임
```



### C: Create

`a1 = Articles()`

`a1.title = 'char'`

`a1.content = 'text'`

ㄴ==  `a1 = Aricles(title='char', content='text')`

`a1.save()`  *# db에 반영*



### R: Read

1. 전체 목록

   `Articles.object.all()`  *# return queryset*

2. 단일 조회

   `Articles.object.get(pk='int')`  *# return object*



### U: Update

`a1 = Articles.object.get(pk=1)`

`a1.title = 'char char'`

`a1.save()`



### D: Delete

`a1 = Articles.object.get(pk=1)`

`a1.delete()`



<b>views.py</b>

```python
from .models import Articles  # class이름
```



## ORM

objects.filter(title__contains=keyword) : keyword를 포함한 제목

objects.order_by('-pk') : pk를 내림차순으로 정렬



## 필터

`|linebreaksbr` : textarea 같은 내용에 줄바꿈 포함돼서 출력
