# Axios_01_Basic



## Axios

Promise 기반 HTTP 클라이언트



### 새로고침 없이 팔로우, 팔로워 수 표시하기

1. 팔로우 버튼이 있는 form의 id 잡기

   ```html
   <form id='followForm'>
       {% csrf_token %}
       <input id='followBtn' type='submit' value='언팔로우'>
       // ...
   </form>
   
   <script>
       const followForm = document.querySelector('#followForm')
   </script>
   ```

   

2. followForm에 이벤트 걸어주기

   ```html
   <script>
   	followForm.addEventListener('submit', function (event) {
           event.preventDefault() // 새로고침 막기
       })
   </script>
   ```

   

3. 이벤트 함수에 axios 작성하기

   ```html
   <script>
       const csrftoken = document.querySelector('[name=csrfmiddlewaretoken]').value
       // ...
   	followForm.addEventListener('submit', function (event) {
           event.preventDefault() // 새로고침 막기
           axios({
               method: 'post',
               url: "{% url 'accounts:follow' person.pk}",
               headers: {'X-CSRFToken: csrftoken'}
           })
       })
   </script>
   ```

   

   - person.pk

     ```python
     def profile(request, username):
         person = get_object_or_404(get_user_model(), username=username)
     ```

   

4. axios로 요청 보내는 url의 콜백함수 작성하기

   ```python
   @require_POST   
   def follow(request, user_pk):
       me = request.user
       you = get_object_or_404(get_user_model(), pk=user_pk)
   
       if me != you:
           if you.followers.filter(pk=me.pk).exists():
               you.followers.remove(me)
               is_follow = False
           else:
               you.followers.add(me)
               is_follow = True
           
           dict_data = {
               'followersCount': you.followers.count(),
               'followingsCount': you.followings.count(),
               'isFollow': is_follow
           }
           return JsonResponse(dict_data)
   ```

   

5. axios promise 작성하기

   ```html
   axios({
         method: 'post',
         url: followUrl,
         headers: {'X-CSRFToken': csrftoken}
       })
       .then(response => {
         followers.innerText = response.data.followersCount
         followings.innerText = response.data.followingsCount
         followBtn.value = response.data.isFollow ? '언팔로우' : '팔로우'
       })
       .catch(error => console.log(error))
   ```

    



### for문으로 돌려지는 경우

1. for문으로 생성되는 폼을 모두 잡는다.

   ```html
   {% for article in articles %}
         <form class="like-form" data-article-id="{{ article.pk }}">
   
   <script>
   	const likeForms = document.querySelectorAll('.like-form')
   </script>
   ```

   

2. forEach로 각 폼에 이벤트를 걸어준다.

   ```html
   <script>
   	likeForms.forEach(likeForm => {
           likeForm.addEventListener('submit', function (event) {
               event.preventDefault()
           })
       })
   </script>
   ```

   

3. axios 작성

   ```html
   <script>
       const csrftoken = document.querySelector('[name=csrfmiddlewaretoken]').value
       // ...
   	likeForms.forEach(likeForm => {
           likeForm.addEventListener('submit', function (event) {
               event.preventDefault()
               axios({
                   method: 'post',
                   url: `/articles/${likeForm.dataset.articleId}/likes/`,
                   headers: {'X-CSRFToken:csrftoken'}
               })
           })
       })
   </script>
   ```

   

   - url
     1번에 폼을 보면 data-article-id로 잡은 것이 있다. script에선 article-id는 빼기 연산이므로 자동으로 articleId로 변경해서 사용할 수 있다. - 뒤에 문자가 대문자로 바뀌는 것. 다만 앞에 dataset이 붙는다. element.dataset.articleId

     ```html
     <form class="like-form" data-article-id="{{ article.pk }}">
         // ...
         <script>
             url: `/articles/${likeForm.dataset.articleId}/likes/`,
         </script>

   

4. axios가 요청 보내는 url의 콜백함수 작성

   ```python
   from django.urls import reverse
   
   @require_POST
   def likes(request, article_pk):
       article = get_object_or_404(Article, pk=article_pk)
       is_login = False
       if request.user.is_authenticated:
           is_login = True
           if article.like_users.filter(pk=request.user.pk).exists():
               article.like_users.remove(request.user)
               is_like = False
           else:
               article.like_users.add(request.user)
               is_like = True
           dict_data = {
               'likeUsersCount': article.like_users.count(),
               'isLike': is_like,
               'isLogin': is_login
           }
           return JsonResponse(dict_data)
       
       else:
           url = reverse('accounts:login')
           dict_data = {
               'isLogin': is_login,
               'url': url
           }
           return JsonResponse(dict_data)
   ```

   

   - from django.urls import reverse
     views.py에서 템플릿의 url name을 사용해서 url 경로를 설정할 수 있다.

     ```python
     from django.urls import reverse
     //...
     	else:  // 비로그인 일때
             url = reverse('accounts:login')
             dict_data = {
                 'isLogin': False,
                 'url': url
             }
             return JsonResponse(dict_data)
     ```

     

5. axios promise 작성

   ```html
   .then(response => {
             if (response.data.isLogin) { // 로그인 O
               const articleId = likeForm.dataset.articleId
               const likeBtn = document.querySelector(`#like-${articleId}`)
               const likeUsers = document.querySelector(`#like-count-${articleId}`)
               
               likeUsers.innerText = response.data.likeUsersCount
               likeBtn.innerText = response.data.isLike ? '좋아요 취소' : '좋아요'
             } else { // 로그인 X
               window.location = response.data.url
             }
           })
   .catch(error => console.log(error))
   ```

   