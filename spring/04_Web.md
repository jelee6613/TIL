# Spring_04_Web

## 정적 컨텐츠

1. 웹브라우저에서 uri를 찾는다. (ex. localhost:8080/hello-static.html)
2. 내장 톰캣 서버에서 스프링 컨테이너에 관련 컨트롤러를 찾는다.
3. 없으면 resource/static에서 찾는다.
4. 응답


## MVC와 템플릿 엔진


## API

### @ResponseBody 사용 원리

1. 웹브라우저에서 uri를 찾는다.
2. 내장 톰캣 서버에서 스프링 컨테이네엇 관련 컨트롤러를 찾는다.
3. @ResponseBody가 붙어있다!
  - HTTP의 BODY에 문자 내용을 직접 반환
  - viewResolver 대신에 HttpMessageConverter가 동작
4. 객체를 반환하자. (default: JSON)