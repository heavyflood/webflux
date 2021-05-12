# Spring Webflux

> Spring Webflux는 복수개의 서비스로 이루어진 분산 시스템이 정상 상황 뿐만 아니라 장애 상황에서도 일관된 동작을 보장해 주는 시스템이며 Microservice가 지향하는 방향이다


## 용도

- 비동기 - 논블록킹 리엑티브 개발에 사용

- 효율적으로 동작하는 고성능 웹 어플리케이션 개발

- 서비스 간 호출이 많은 마이크로서비스 아키텍쳐에 적합

## 개발방식

    - MVC (@Controller, @RestController, @RequestMapping)
    
    - 새로운 함수형 모델 : 새로운 요청 - 응답 모델
    
    - 서블릿 스택과 API에서 탈비 (Servlet API는 리엑티브 함수형 스타일에 적합하지 않음)

- ServerRequest, ServerResponse

## 지원 웹 서버 / 컨테이너

    - Servlet 3.1 (Tomcat, Jetty, ..)
    
    - Netty
    
    - Undertow

## Handler Function

    - 함수형 스타일의 웹 핸들러 (컨트롤러 메소드)
    
    - 웹 요청을 받아 웹 응답을 돌려주는 함수

## 함수형 Webflux가 웹 요청을 처리하는 방식

    - 요청 매핑: RouterFunction - url 같은 정보로 어떤 핸들러가 이 요청을 처리할지 결정함
    
    - 요청 바인딩 - Handler Function
    
    - 핸들러 실행 - HandlerFunction
    
    -핸들러 결과 처리 (응답 생성) - HandlerFunction

## Spring MVC와 다른점

    - Spring MVC는 Java EE의 Servlet spec에 기반하여 만들어져 있고, 본질적으로 블럭킹 동기방식이다
    
    - 비동기 방식이 있지만 서블릿은 응답을 기다리는 동안 pool의 쓰레드들을 여전히 지연시킬 수 있기 때문에 전체 stack 이 reactive 해야 한다
    
    - 스프링 프레임워크 5에 Webflux가 도입됐다.
    
    - MVC는 서블릿 컨테이너와 서블릿을 기반으로 웹 추상화 계층을 제공
    
    - Webflux는 서블릿 컨테이너 뿐만 아니라 Netty, Undertow와 같은 네트워크 어플리케이션 프레임워크도 지원하므로 HTTP와 Reactive Stream 기반으로 웹 추상화 계층을 제공합니다
    
    - 따라서 Webflux 모듈에 HTTP abstractions, Reactive Stream adapter, Reactive codes 그리고 non-blocking servlet api를 지원하는 core web api가 포함되어 있습니다.
    
    - 따라서 server-side webflux 상에서 두 가지 프로그램 모델로 구성이 가능합니다.
    
    - annotated Controller: Spring MVC 모델 기반의 기존 spring-web 모듈과 같은 방식으로 구성하는 방법으로 Spring MVC에서 제공하는 어노테이션들을 그대로 사용가능합니다
    
    - Functional Endpoints: Java 8 lambda style routing과 handling 방식입니다. 가벼운 routing 기능과 request 처리 라이브러리. callback 형태로써 요청이 있을 때만 호출된다는 점이 nnotated controller과 다름

## 동작 흐름

    - Spring MVC는 서블릿 컨테이너로 들어온 요청이 디스패처 서블릿으로 전달되면, 시스패처 서블릿은 순차적으로 HandlerMapping, HandlerAdapter에 요청에 대한 처리를 위임하고, ViewResolver에 응담에 대한 처리를 위임하는 방식
    
    - Webflux도 크게 다르지 않음
    
    - 웹 서버 (Servlet Container, Netty, Undertow, etc)로 들어온 요청이 HttpHandler에서 전달되면 HttpHandler는 전처리 후 WebHandler에 처리를 위임하게 된다. 이 WebHandler 내부에서 HandlerMapping, HandlerAdapter, HandlerResultHandler 3개의 컴포넌트가 요청과 응답을 처리하게 됩니다. 처리가 끝나면 HttpeHandler가 후처리 후 응답을 종료합니다.
    
    - Spring MVC와 동일하게 컴포넌트가 존재하지만 동작 방식이 달라 서로 다른 인터페이스를 사용합니다.
