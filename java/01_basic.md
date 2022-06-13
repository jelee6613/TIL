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



## 형변환

- byte < short < int < long < float < double
- 묵시적(암묵적) : Implicit Casting
  - 범위가 넓은 데이터 형에 좁은 데이터 형을 대입하는 것
- 명시적 : Explicit Casting
  - 범위가 좁은 데이터 형에 넓은 데이터 형을 대입하는 것
  - 형변환 연산자 사용 - (타입) 값;

```java
// 작은집에서 큰집으로 이사갈때는 문제가 없다. (묵시적)
short sa = 32767;
int c = sa;
// 큰집에서 작은집으로 갈떄는.. 컨펌이 필요하다. (명시적)
short sb = (short) c;
// 같은 크기의 집이라도 컨펌이 필요한 경우 (명시적)
float f = 10;
int g = (int) f;
```

