# Spring_01_Basic



## Spring Framework 특징

- POJO (Plain Old Java Object) - 일반적인 자바 객체를 이용해서 그대로 사용할 수 있음을 의미한다.
- 의존성 주입 (Dependency Injection)을 통한 객체관계 구성
- 관점지향 프로그래밍 (AOP, Aspect Oriented Programming) 지원
- 제어 역전 (IoC, Inversion of Control)
- 높은 확장성과 다양한 라이브러리 지원



## 왜 Spring Framework?

- Spring is everywhere : 전세계 많은 개발자들이 사용하고 있다.
- Spring is flexible : 유연하고 포괄적인 외부 라이브러리 확장을 통해 다양한 형태의 애플리케이션 개발가능
- Spring is productive : Spring boot는 프로그래밍 접근 방식을 변환하여 작업량을 줄여준다.
- Spring is secure : 업계 표준 보안 체계와 쉽게 통합할 수 있고, 기본적으로 신뢰할 수 있는 솔루션을 제공한다.
- Spring is supportive : 커뮤니티가 잘 발달해 있으며, 빠른 시작, 가이드, 자습서 등의 리소스를 지원하고있다.


## 프로젝트 생성
<a href="start.spring.io">start.spring.io</a>
  - Project: Gradle
  - Language: Java
  - Project Metadata
    - Group: 도메인명
    - Artifact: 빌드 결과물, 프로젝트명
  - Dependencies
    - Spring Web
    - Thymeleaf
  - GENERATE !!


## MVC 구조

- Model
  - 모든 데이터 정보를 가공하여 가지고 있는 컴포넌트
  - 사용자가 이용하려는 모든 데이터를 가지고 있어야하며, View 또는 Controller에 대해 어떠한 정보도 알 수 없어야 한다.
  - 변경이 일어나면 처리 방법을 구현해야한다.

- View
  - 시각적인 UI 요소를 지칭하는 용어
  - Model이 가지고 있는 데이터를 저장하면 안된다.
  - Model이나 Controller에 대한 정보를 알면 안되며 단순히 표시를 해주는 역할
  - 변경이 일어나면 처리 방법을 구현해야한다.

- Controller
  - Model과 View를 연결
  - Model 또는 View의 변경을 인지하여 대처를 해야한다.

### MVC 동작 순서

1. 클라이언트가 서버에 요청하면 front Controller인 DispatcherServlet 클래스가 요청을 받는다.
2. DispatcherServlet은 프로젝트 파일 내의 servlet-context.xml 파일의 @Controller 인자를 통해 등록한 요청 위임 컨트롤러를 찾아 mapping된 Controller가 존재하면 @RequestMapping을 통해 요청을 처리할 메소드로 이동한다.
3. Controller는 해당 요청을 처리한 Service를 받아 비즈니스 로직을 Service에게 위임한다.
4. Service는 요청에 필요한 작업을 수행하고, 요청에 대해 DB에 접근해야한다면 DAO에 요청하여 처리를 위임한다.
5. DAO는 DB정보를 DTO를 통해 받아 Service에게 전달한다.
6. Service는 전달받은 데이터를 Controller에게 전달한다.
7. Controlloer는 Model 객체에게 요청에 맞는 View 정보를 담아 DispatcherServlet에게 전송한다.
8. DispatcherServlet은 ViewResolver에게 전달받은 View 정보를 전달한다.
9. ViewResolver는 응답할 View에 대한 JSP를 찾아 DispatcherServlet에게 전달한다.
10. DispatcherServlet은 응답할 뷰의 Render를 지시하고 View는 로직을 처리한다.
11. DispatcherServlet은 클라이언트에게 Rending된 View를 응답하며 요청을 마친다.

## Spring 구조
- Controller : 웹 MVC의 컨트롤러 역할
- Service : 핵심 비즈니스 로직 구현
- Repository : DB에 접근, 도메인 객체를 DB에 저장하고 관리
- Domain : 비즈니스 도메인 객체, 예) 회원, 주문, 쿠폰 등등 주로 DB에 저장하고 관리 