---
layout: post
title: "토비 스프링 스터디 1주차"
date:   2019-09-06
categories: Spring
comments: false
---

* DispatcherServlet
* 플래시맵
* EhCache
* 템플릿 메서드 패턴
* 팩토리 메소드 패턴, 왜 쓰느냐
* 전략 패턴
* 솔리드(SOLID)
* 서블릿
* 어플리케이션 컨텍스트
* 빈 스코프
* 싱글톤 패턴 / 싱글톤 레지스터리

<br/>

## DispatcherServlet

* Dispatch : '보내다' 라는 뜻.

클라이언트로부터 어떠한 요청이 오면 Tomcat 같은 'ServletContainer'  가 요청을 받는데, **이때 제일 앞에서 서버로 들어오는 모든 요청을 처리하는 프론트 컨트롤러를 Spring 에서 정의 하였고, 이를 Dispatcher Servlet 이라고 한다.**

* 공통 처리 작업을 DispatcherServlet 이 처리한 후, 적절한 세부 컨트롤러로 작업을 위임.
* DispatcherServlet 이 처리하는 URL 패턴을 지정한다. ('/*.do' 와 같은 '/' 로 시작하며, '.do' 로 끝나는 URL 패턴에 대한 처리를 하라고 지정)

> ### Front Controller?
>
> 주로 서블릿 컨테이너 제일 앞에서 서버로 들어오는 클라이언트의 모든 요청을 받아서 처리해주는 컨트롤러, MVC 구조에서 함께 사용되는 패턴.
>
> * 프론트 컨트롤러를 Spring 에서 'Dispatcher Servlet' 이라고 한다

* Sevlet 3.0 이상에서부터 'WebApplicationInitializer' 구현 또는 'AbstractAnnotaionConfigDispatcherServletInitializer' 상속으로 'web.xml' 에서 하던 설정을 java config 로 설정할 수 있다. 
* java config 를 통해 설정하여 classpath 내에 두면,  'SpringServletContainerInitializer' 가 서블릿을 초기화 할 때 감지한다.

<br/>

1. DispatcherServlet 이 없었을 때는, 'web.xml' 에서 모든 서블릿에 대해 URL 매핑을 위해 모두 등록해주었어야 한다.
2. DispatcherServlet 이 해당 어플리케이션으로 들어오는 모든 요청을 핸들링 해주면서 작업이 편리해짐.
3. '@MVC' 사용이 가능해짐.
4. 모든 요청을 처리하다 보니, 이미지나, HTML 파일을 불러오는 요청마저 전부 Controller 로 넘기는 문제가 발생.
5. 접근 URL 을 따로 두어 (ex, '/app', '/resource') 동적 파일과 정적 파일 처리를 나눔.
6. 모든 요청에 대해 위 URL 을 붙여주어야 해서 직관적이지 못하고, 코드도 깔끔하지 못함.
7. Spring은 '<mvc:resources/>' 를 이용해서 위 문제를 해결. (프레임워크 상에서 '/src', '/resources' 디렉터리 따로 있는 것)
8. DispatcherServlet 에서 해당 요청에 대한 컨트롤러를 찾을 수 없는 경우에, 2차적으로 설정된 경로에서 요청을 탐색하여 자원을 찾아내는 것.
9. 영역을 분리함으로써 효율적인 리소스 관리를 지원하고 추후에 확장을 용이하게 해줌.

*참고
[DispatcherServlet 동작 원리](https://jess-m.tistory.com/15)



<br/>

## 플래시맵 (Flash Map)

Controller 에서 'redirect' 해야하는 경우에, 특정 데이터를 넘겨야 할 때가 있다. 2가지 방법이 있는데, request parameter 로 URL 로 넘겨주는 'addAttribute' 와  세션에 저장한 후 retrive 되면 세션에서 바로 삭제하는 'addFlashAttribute' 가 있다. 'FlashMap' 을 이용해 넘길 데이터를 세션에 저장하고 redirect 되어 데이터를 받게되면 바로 삭제한다.

* 플래시 어트리뷰트 (Flash Attribute) 를 저장하는 맵 (Map)
* 플래시 어트리뷰트 : 하나의 요청에서 생성되어, 다음 요청으로 전달되는데, 한번 사용 후 바로 제거

~~~java
@RequestMapping("/info/test")
public String tests(RedirectAttributes redirectAttributes) {
    redirectAttributes.addFlashAttribute("isNewUser", true);
    return "redirect:/";
}
~~~

