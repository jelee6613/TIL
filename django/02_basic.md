# Django_02_Basic

![image-20220303210609739](https://github.com/jelee6613/TIL/tree/master/img/image-20220303210609739.png) 

최상위 templates 폴더를 만들어서 기본 뼈대 레이아웃 html 을 구축하자!

매번 html 생성할 때마다 ! + tab 구조의 반복을 피하기 위해 base.html 의 ! + tab 구조를 잡고, 앞으로 생성되는 html에 `{% extends 'base.html' %}` 작성하여 가져와 쓴다.

---





![image-20220303210816851](../../AppData/Roaming/Typora/typora-user-images/image-20220303210816851.png)

app > templates > app이름 구조

애플리케이션의 templates에  애플리케이션명 폴더를 만든다. 그러지 않으면 다른 애플리케이션에 같은 이름의 html이 있을 경우, `settings.py` 에 먼저 등록된 애플리케이션의 html을 불러온다.

---



![image-20220303211236289](../../AppData/Roaming/Typora/typora-user-images/image-20220303211236289.png)





form GET 을 이용한 ping -> pong :ping_pong:

`ping.html`에 form을 작성하는데 action의 url 주소를 pages:pong으로 작성하면, 

![image-20220303212213641](../../AppData/Roaming/Typora/typora-user-images/image-20220303212213641.png)

pages/ping/ 에서 id와 password를 입력하고 로그인을 누르면 action에 입력된 pages:pong으로 이동하고, 



![image-20220303211304610](../../AppData/Roaming/Typora/typora-user-images/image-20220303211304610.png)



views.py에 작성된 def pong에 따르면 form 에서 수집된 정보를 변수화하여 context를 이용하여 다음과 같이 출력할 수 있다.

![image-20220303212418473](../../AppData/Roaming/Typora/typora-user-images/image-20220303212418473.png)

![image-20220303212428466](../../AppData/Roaming/Typora/typora-user-images/image-20220303212428466.png)