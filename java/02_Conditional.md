# Java_02_Conditional



## if

```java
int score = 75;
		
if (score > 90) {
    System.out.println("A");
} else if (score > 80) {
    System.out.println("B");
} else if (score > 70) {
    System.out.println("C");
} else {
    System.out.println("F");
}
```







## switch



```java
int month = 5;
		
switch(month) {
    case 1:
    case 2:
    case 12:
        System.out.println("겨울");
        break;
    case 3:
    case 4:
    case 5:
        System.out.println("봄");
        break;
    case 6:
    case 7:
    case 8:
        System.out.println("여름");
        break;
    case 9:
    case 10:
    case 11:
        System.out.println("가을");
        break;
}
```





switch () 괄호 안에 변수 or 정수를 입력하고, {} 블록 안에 case 값이 일치하면 해당 case 구문 아래에 있는 식을 실행한다.

`break`를 입력하지 않으면 실행되는 case 구문을 시작으로 아래에 있는 모든 식이 실행된다.