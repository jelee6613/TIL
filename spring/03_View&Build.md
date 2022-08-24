# Spring_03_View & Build

- Welcome Page
  - src > main > resources > static > index.html
  ```html
  <!DOCTYPE HTML>
  <html xmlns:th="http://www.thymeleaf.org">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport"
            content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
      <meta http-equiv="Content-Type" content="text/html">
      <title>Document</title>
  </head>
  <body>
  <p th:text="'안녕하세요. ' + ${data}">안녕하세요. 손님</p>
  </body>
  </html>
  ```

- Controller
  - src > main > java > hello.hellospring > controller(package) > HelloController(class)
  ``` java
  package hello.hellospiring.controller;

  import org.springframework.stereotype.Controller;
  import org.springframework.ui.Model;
  import org.springframework.web.bind.annotation.GetMapping;

  @Controller
  public class HelloController {

      @GetMapping("hello")
      public String hello(Model model) {
          model.addAttribute("data", "hello!!");
          return "hello";
      }
  }
  ```

- Build
  ```bash
  ~/hello-spring

  $ ./gradlew build
  $ cd build
  $ cd libs
  $ java --jar hello-spiring-0.0.1-SNAPSHOT.jar