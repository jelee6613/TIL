# Django_11_Serializer(1:N)



## PrimaryKeyRelatedField

- pk를 사용해서 관계 대상을 나타내는데 사용
- 필드가 to many relationships(N)를 나타내면 `many=True`
- comment_set 필드 값을 form-data로 받지 않으므로 `read_only=True`



```python
# serializers.py

class ArticleSerializer(serializers.ModelSerializer):
    # 모델명_set
    comment_set = serializers.PrimaryKeyRelatedField(many=True, read_only=True)
    
    class Meta:
        model = Article
        fields = '__all__'
```



- models.py에서 ForeignKey 작성시 related_name 설정하면 comment_set 대신 comments 등으로 가능

  ```python
  # models.py
  
  class Comment(models.Model):
      article = models.ForeignKey(Article, on_delete=models.CASCADE, related_name='comments')
  ```

  