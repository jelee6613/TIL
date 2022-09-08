# Java_07_Inheritance



## Inheritance

1. 확장성, 재사용성
2. 클래스 선언 시 extends 키워드를 명시
3. 관계
   - 부모 (상위, Super) 클래스 : Person
   - 자식 (하위, Sub) 클래스 : Student
4. 자식 클래스는 부모 클래스의 멤버변수, 메소드를 자신의 것처럼 사용할 수 있다.
5. Object 클래스는 모든 클래스의 조상 클래스
   - 별도의 extends 선언이 없는 클래스는 기본값으로 extends Object 



### Code

```java
class Person {
    String name;
    int age;
    
    // 매개변수가 있으므로 기본생성자가 자동으로 생기지 않는다.
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
        System.out.println("Person 클래스의 생성자")
    }
}

class Student extends Person {
    String major;
    
    public Student(String name, int age, String major) {
        super(name, age); // 2
        this.major = major;
        System.out.println("Child 클래스의 생성자")
    }
}

public class ExtendsTest {
    public static void main(String[] args) {
        Student c = new Student();  // 1
    }
}

/*
Person 클래스의 생성자
Student 클래스의 생성자
*/
```

1. 자식클래스 객체를 생성하는 것은, 부모클래스 객체를 먼저 선언하고, 자식클래스를 이어 붙여서 생성한다.
2. 자식클래스 생성자에선 기본적으로 부모클래스 기본생성자를 호출한다.
   부모클래스 기본생성자가 없으면 명시적으로 super 키워드를 이용해 부모클래스 생성자를 호출해야 한다.



## getter & setter

### getter

- get + 대상변수명을 이름으로 하는데, 단어가 붙으면 첫글자 대문자 (ex. getName)

- 매개변수 X

- 반환유형은 대상변수의 타입

- 대상변수 값 리턴

  ```java
  public String getName() {
      return name;  // 대상 변수 값 리턴
  }
  ```



### setter

- set + 대상변수명을 이름으로 하는데, 단어가 붙으면 첫글자 대문자 (ex. setName)

- 매개변수 O (대상변수와 같은 타입의 변수)

- 반환유형은 void

- 매개변수로 받은 값을 대상변수에 넣어주는 것

  ```java
  public void setName(String name) {
      this.name = name;
  }
  ```

  



```java
package 상속;

class Parent {
    int data = 10;
    public void print() {
        System.out.println(data);
    }
}

class Child {
    int data = 20;
    public void print() {
        int data = 30;
        System.out.println(data);        // 30
        System.out.println(this.data);   // 20
        System.out.println(super.data);  // 10
    }
}

public class ExtendsTest {
    public static void main(String[] args) {
        Parent p = new Child();
        
        // 고개를 들어 왼쪽을 보라, Parent의 data
        System.out.println(p.data);
        
        // 함수는 예외로 동적 바인딩이 일어나 Child의 print가 실행된다.
        p.print();  // 30 20 10
    }
}
```
