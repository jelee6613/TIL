# Java_05_Class



## Class

- 관련있는 변수와 함수를 묶어서 만든 사용자정의 <자료형>
- 모든 객체들의 생산처
  - 객체 : 하나의 역할을 수행하는 '메소드와 변수(데이터)'의 묶음
- 프로그래밍이 쓰이는 목적을 생각하여 어떤 객체를 만들어야 하는지 결정한다.
  - 객체지향 프로그래밍 : 프로그램을 단순히 데이터와 처리 방법으로 나누는 것이 아니라, 프로그램을 수많은 '객체(object)'라는 기본 단위로 나누고 이들의 상호작용으로 서술하는 방식
- 각 객체들이 어떤 특징(속성과 동작)을 가지고 있을지 결정한다.
- 객체들 사이에서 메시지를 주고 받도록 만들어 준다.



```java
public class Person {
    String name;
    int age;
    int height;

    // 생성자 - 생성자명은 클래스명과 같음
    Person(String n, int a, int h) {
        System.out.printIn("나 불렀니?")
        name = n;
        age = a;
        height = h;
    }
	
    // 메소드 오버로딩 : 이름이 같고 매개변수가 다른 메소드를 여러개 정의하는 것
    // 일치하는 매개변수를 가지는 메소드를 실행한다.
    void print() {
        System.out.printf("이름은 %s이고, 나이는 %d살, 키는 %d cm입니다.", name, age, height);
    }
   
    void print(int n) {
        System.out.printf("나는 정수: %d", n);
    }
    
    void print(double n) {
        System.out.printf("나는 실수: %d", n);
    }
    
}
```



## 생성자

- 객체가 생성될때 최초 한번 수행되는 함수

- 생성자라는 함수의 이름은 클래스명과 같다.

- 생성자는 반환 유형이 없다.

- 생성자를 만들지 않으면, 몸통이 비어있는 기본 생성자를 컴파일러가 자동으로 생성해준다.

- 생성자를 만들면 기본 생성자는 자동으로 생성되지 않으므로 원하면 직접 만들어야 한다.

- 오버로딩을 지원한다.

  ```java
  class Dog {
      String name;
      int age;
      
      Dog() {}
      
      Dog(String n) {
          name = n;
      }
      
      Dog(int a) {
          age = a;
      }
      
      Dog(String n, int a) {
          name = n;
          age = a;
      }
  }
  
  //////
  
  class Main {
      public static void main(String [] a) {
          Dog d1 = new Dog();
          Dog d2 = new Dog("래시");
          Dog d3 = new Dog(14);
          Dog d4 = new Dog("래시", 14);
      }
  }
  ```

  



## 메소드 오버로딩

- 이름이 같고 매개변수가 다른 메소드를 여러개 정의하는 것
- 매개변수가 일치하는 메소드를 실행한다.

```java
class Movie {
    String title;
    double rate;
    
    Movie(String t, double r) {
        title = t;
        rate = r;
    }
    
    // 메소드 오버로딩
    void print() {
		System.out.println("영화 제목:" + title + "평점:" + rate);
	}
    
    void print(String t) {
        System.out.println(t);
    }
    
    void print(double r) {
        System.out.println(r);
    }
}
```



## this

```java
public class ExDate {
	int year;
	int month;
	int day;
	
	ExDate(int year, int month, int day) {
		this.year = year;
		this.month = month;
		this.day = day;
	}
	
	ExDate() {}
	
	void showDate() {
		System.out.println(this.year + "년" + this.month + "월" + this.day + "일");
	}
}

/////

ExDate ex01 = new ExDate();
ex01.showDate();  // "0년0월0일"

ExDate ex02 = new ExDate(2022, 6, 21);
ex02.showDate();  // "2022년6월21일"
```



## static

- 객체를 생성하지 않아도 존재하는 변수나 함수



1. 로딩 시점
   - static : 클래스 로딩 시
   - non-static : 객체 생성 시
2. 메모리상의 차이
   - static : 클래스당 하나의 메모리 공간만 할당
   - non-static : 인스턴스 당 메모리가 별도로 할당
3. 문법적 특징
   - static : 클래스 이름으로 접근
   - non-static : 객체 생성 후 접근



## 기능을 위한 class

```java
// Student.java

public class Student {
    String name;
    String major;
    int age;
    
    public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public String getMajor() {
		return major;
	}
	public void setMajor(String major) {
		this.major = major;
	}
	public int getAge() {
		return age;
	}
	public void setAge(int age) {
		this.age = age;
	}
}
```



```java
// StudentManager.java

public class StudentManager {
    int size = 0;
    Student[] students = new Students[100];
    
    void addStudent(Student s) {
        students[size++] = s;
    }
    
    void changeMajor(String name, String major) {
        Student s = getStudent(name);
        if (s == null) {
            System.out.println("No result")
        } else {
            s.setMajor(major);
        }
    }
    
    Student getStudent(String name) {
        int idx = -1;
        
        for (int i = 0; i < size; i++) {
            if (name.equals(students[idx].getName())) {
                idx = i;
                break;
            }
        }
        
        if (idx == -1) {
            return null;
        } else {
            return students[idx];
        }
    }
}
```



```java
// StudentTest.java

import java.util.Scanner;

public class StudentTest {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        StudentManager sm = new StudentManager();
        int sel;
        
        do {
            System.out.println("번호로 입력하세요.");
			System.out.println("1. 학생추가");
			System.out.println("2. 학생조회");
			System.out.println("3. 전공변경");
			System.out.println("0. 종료");
            
            sel = sc.nextInt();
            
            if (sel == 1) {
                System.out.println("이름: ");
                String name = sc.next();
                
                System.out.println("나이: ");
				int age = sc.nextInt();
				
				System.out.println("전공: ");
				String major = sc.next();
                
                Student s = new Student();
                s.setName(name);
                s.setAge(age);
                s.setMajor(major);
                
                sm.addStudent(s)
                    
            } else if (sel == 2) {
                System.out.println("학생을 조회합니다.");
				System.out.println("이름: ");
                String name = sc.next();
                Student s = sm.getStudent(name);
                
                if (s == null) {
                    System.out.printIn("No result");
                } else {
                    System.out.println("이름: " + s.getName());
                    System.out.printIn("나이: " + s.getAge());
					System.out.println("전공: " + s.getMajor());
                }
            } else if (sel == 3) {
				System.out.println("전공을 변경합니다.");
				System.out.println("이름: ");
				String name = sc.next();
				System.out.println("전공: ");
				String major = sc.next();
				
				sm.changeMajor(name, major);
            }
        } while (sel != 0);
    }
}
```





## 추상클래스(abstract class)

- 자손클래스의 메소드만 사용되어 부모클래스의 메소드 구현은 무의미할 때, 부모를 추상화
- 부모클래스 메소드의 선언부만 남기고 구현부는 ;(세미콜론)으로 대체
- 구현부가 없으므로 abstract 키워드를 메소드 선언부에 작성
- abstract 메소드가 하나라도 있으면 class 선언부에도 abstract 작성
- 부모클래스 메소드가 추상메소드면 자식클래스는 해당메소드를 구현해야만 하는 의무를 가진다.
- 추상클래스(abstract class)는 미완성이기 때문에 객체를 생성할 수 없다. (단, 1회용 구현 예외)



```java
public abstract class Chef {
    String name;
    int age;
    String spectiality;
    
    public void eat() {
        System.out.println("음식을 먹는다.")
    }
    
    public abstract void cook();
}

public class KFoodChef extends Chef {
    
    @Override
    public void cook() {  // 부모클래스에서 추상메소드이기 때문에 무조건 구현해야 하는 메소드
        System.out.println("한식을 조리합니다.")
    }
}

public class ChefTest {
    public static void main(String[] args) {
        Chef c1 = new KFoodChef();
        c1.cook();
        
        // 추상클래스는 미완성이기 때문에 객체를 생성할 수 없지만 추상메소드를 작성하면 1회용 구현
        Chef c2 = new Chef() {
            
            // 익명클래스 문법으로 1회용 구현과 함께 객체화 가능
            @Override
            public void cook() {
                System.out.println("추상메소드 1회용 구현")
            }
            
            @Override
            public void eat() {
        		System.out.println("음식을 먹는다.")
    		}
        }
    }
}
```





## 인터페이스(interface)



### 필요성

- 구현의 강제로 표준화 처리 (abstract 메소드 사용)
- 인터페이스를 통한 간접적인 클래스 사용으로 손쉬운 모듈 교체 지원
- 서로 상속의 관계가 없는 클래스들에게 인터페이스를 통한 관계 부여로 다형성 확장
- 모듈 간 독립적 프로그래밍 가능 -> 개발 기간 단축





1. interface 키워드를 이용하여 선언

   ```java
   public interface MyInterface {}
   ```

2. 선언되는 변수는 모두 상수로 적용

   ```java
   public static final int MEMBER1 = 10;
   int MEMBER2 = 10;
   ```

3. 선언되는 메소드는 모두 추상 메소드로 적용

   ```java
   public abstract void method1(int param);
   void method2(int param);
   ```

4. 객체 생성이 불가능 (추상클래스와 동일한 특성)

5. 클래스가 인터페이스를 상속할 경우 extends가 아닌 implements 키워드를 이용

   ```java
   interface Shape {}
   
   class Circle extends Shape {}     // X
   class Circle implements Shape {}  // O
   ```

6. 인터페이스를 상속받는 하위클래스는 추상 메소드를 반드시 오버라이딩(재정의) 해야 한다.

7. 인터페이스 다형성 적용

   ```java
   public static void main(String[] args) {
       Chef chef = new KFoodChed();
   }
   ```

   
