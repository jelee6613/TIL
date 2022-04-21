# Django_08_ManyToMany





## ManyToMnayField

```python
class Doctor(models.Model):
    # patients = models.ManyToManyField(Patient)  # 복수형
    name = models.TextField()

    def __str__(self):
        return f'{self.pk}번 의사 {self.name}'
 

class Patient(models.Model):
    name = models.TextField()
    doctors = models.ManyToManyField(Doctor)  # 복수형
    
    def __str__(self):
        return f'{self.pk}번 환자 {self.name}'
```



* add()
* remove()



## Arguments

### related_name

* 역참조에 사용하는 매니저의 이름을 설정

```python
class Doctor(models.Model):
    name = models.TextField()

    def __str__(self):
        return f'{self.pk}번 의사 {self.name}'
 

class Patient(models.Model):
    name = models.TextField()
    doctors = models.ManyToManyField(Doctor, related_name='patients')  # 복수형
    
    def __str__(self):
        return f'{self.pk}번 환자 {self.name}'
```



### through

* 별도의 데이터를 추가하기 위해 커스텀

```python
class Doctor(models.Model):
    name = models.TextField()

    def __str__(self):
        return f'{self.pk}번 의사 {self.name}'
 

class Patient(models.Model):
    name = models.TextField()
    doctors = models.ManyToManyField(Doctor, through='Reservation')
    
    def __str__(self):
        return f'{self.pk}번 환자 {self.name}'
    
class Reservation(models.Model):
    doctor = models.ForeignKey(Doctor, on_delete=models.CASCADE)
    patient = models.ForeignKey(Patient, on_delete=models.CASCADE)
    symptom = models.TextField()
    reserved_at = models.DatetimeField(auto_now_add=True)
```





### symmetrical

```python
followings = models.ManyToManyField("self", symmetrical=False, related_name='followers')
```

1번이 3번을 팔로우하면, 3번도 1번을 자동 팔로우하는 것을 막기 위해 `symmetrical=False` 처리
