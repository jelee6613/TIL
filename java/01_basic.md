# Java_01_Basic



## 시작

### Java Development Kit (openJDK 설치)

1. https://www.azul.com/downloads/?version=java-8-lts&os=windows&architecture=x86-64-bit&package=jdk&show-old-builds=true
   Java 8 (LTS) > Windows > x86 64-bit > JDK > 8u192b01 설치
2. https://www.eclipse.org/downloads/packages/release/2018-09/r
   Eclipse IDE for Java EE Developers 설치
   Windows > Preferences > General > Workspace > Text file encoding > Other > UTF-8 설정





## print

- print : 그냥 출력

- println : 줄바꿈 출력

- printf : 포맷팅 출력

  ```java
  System.out.printf("%d \n", 10);  // 10 
  System.out.printf("%o \n", 10);  // 12
  System.out.printf("%x \n", 16);  // 10
  ```

  



## 자주 사용하는 단축키

- Ctrl + Shift + F : 정렬 (formating)
- Ctrl + Shift + C : 주석처리
- Ctrl + Space : 자동완성



## 변수 선언 & 할당

- type name

  ```java
  int age;  // 선언
  age = 28;  // 할당
  
  int age2 = 25;  // 선언 & 할당
