# Java_03_Loop



## while

```java
int num = 5;

while (num > 0) {
    System.out.printIn("haha");
    num--;
}

// haha 5번 출력
```



## for

```java
for (int num = 3; num > 0; num--) {
    System.out.printIn("hoho");
}

// hoho 3번 출력
```





## do while

```java
Scanner scan = new Scanner(System.in);

int value;

do {
    value = scan.nextIn();
    System.out.printIn("입력받은 수: " + value);
} while (value != 10);

System.out.printIn("드디어 10을 입력했군요.");
```

