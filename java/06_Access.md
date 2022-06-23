# Java_06_Access



## 패키지(package)

- 프로그램의 많은 클래스를 관리하기 위해서 패키지를 이용한다.
- 일반적으로 소속이나 회사의 도메인을 사용한다.
  ex) com.ssafy.project.service



## 임포트(import)

- 다른 패키지에 있는 클래스를 사용하기 위해서는 import 과정이 필요하다.

```java
package com.ssafy.project.service;

import com.ssafy.project.dto.Person;

public class PersonService {
    Person p;
}
```



## 캡슐화(Encapsulation)

- 객체의 속성과 행위를 하나로 묶고, 실제 구현 내용 일부를 외부에 감춘다.





## 접근제한자(access modifier)

- 클래스, 멤버변수, 멤버메서드 등의 선언부에서 접근 허용 범위를 지정하는 역할의 키워드

- public, private, (default), protected 등이 있다.

  - public : 모든 위치에서 접근이 가능
  - private : 자신의 클래스에서만 접근이 허용
  - default : 같은 패키지에만 접근이 허용, 접근제한자 선언이 안 되었을 경우 기본 적용
  - protected : 같은 패키지에서 접근 O, 다른 패키지에서 접근 X
    단, 다른 패키지의 클래스와 상속관계가 있을 경우 접근 가능

  |  수식어   | 클래스 내부 | 동일 패키지 | (다른 패키지내의) 하위 클래스 | 다른 클래스 |
  | :-------: | :---------: | :---------: | :---------------------------: | :---------: |
  |  private  |      O      |             |                               |             |
  | (default) |      O      |      O      |                               |             |
  | protected |      O      |      O      |               O               |             |
  |  public   |      O      |      O      |               O               |      O      |

  

- 그 외 제한자

  - static : 클래스 레벨의 요소 설정
  - final : 요소를 더 이상 수정할 수 없게 함
  - abstract : 추상 메서드 및 추상 클래스 작성



### public & private

- public : 모든 위치에서 접근이 가능
- private : 자신 클래스에서만 접근이 허용



```java
class Car {
    String color;
    private int speed;
    
    public void speedUp() {
        if (speed < 250) {
            this.speed += 10;
        }
    }
    
    // private인 speed를 대신 갖다주는 메소드
    public int getSpeed() {  // getter (접근자)
        return this.speed;
    }
    
    // private인 speed의 값을 변경하는 메소드
    public void setSpeed(int speed) {  // setter (설정자)
        // 변수가 아니라 함수이기 때문에 동작을 수행할 수 있다.
        if (speed > 0 && speed < 250) {
            this.speed = speed;
        }
    }
}

public class CarTest {
    public static void main(String[] args) {
        Car c = new Car();
        c.speedUp();
        // c.speed = 300; private 멤버는 외부에서 접근이 불가하다.
    }
}
```

