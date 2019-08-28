---
layout: post
title: "[Programmers - 웹 백엔드 강의] 사전 질문"
date:   2019-08-28
categories: Spring
comments: false
---

### Q. 아래의 Entity에 해당하는 클래스를 작성해보세요.

---

<img width="867" alt="스크린샷 2019-08-28 오후 7 47 26" src="https://user-images.githubusercontent.com/20623970/63849285-b8a76400-c9cc-11e9-803a-9c73a52b5380.png">

<br/>

public class Users {

​	private BigInteger seq;

​	private String name;

​	private String email;

​	private String password;

​	private String profileImageUrl;

​	private int loginCount;

​	private Date lastLoginAt;

​	private Date createAt;

}

<br/>

### Q. HTTP 요청 메소드들을 나열하고, 각 메소드의 쓰임새를 아는대로 자세히 설명해주세요.

---

GET : 요청을 url 파라미터에 담아서 보내고, 주로 저장소의 데이터를 조회하는데 쓰인다.

POST : 요청을 body에 담아서 보내고, 저장소에 저장할 데이터를 전송하는데 쓰인다.

DELETE : 요청을 파라미터로 보내고, 데이터를 삭제하는 작업에 쓰인다.

PUT : 요청을 파라미터로 보내고, 수정 작업에 사용한다.

<br/>

### Q. RESTful API에 대해서 본인이 지금까지 알고 있었던 범위 내에서 설명해보세요.

---

위 HTTP 요청 메소드들의 쓰임에 맞게 API 를 구성하는 것으로 알고 있습니다.

<br/>

### Q. Transaction 처리에 대해 설명해주세요.

---

데이터를 처리하는 가장 작은 단위.

한번에 처리 할 수 있는 단위를 말하고, 트랜젝션이 처리되는 동안 데이터는 변하면 안된다.

변하거나 변경이 들어오면, 해당 트랜젝션은 전략에 따라 실패하거나, 수정되어 적용되거나, 원래 데이터로 적용되어야 한다.

<br/>

### Q. @Component, @Controller, @Repository, @Service 어노테이션에 대해 알고 있던 만큼 설명해주세요.

---

* @Component : util 성 클래스에 많이 사용했습니다. RestTemplate 를 생성하는 클래스나, 파싱을 위한 클래스를 만들었을 때 서비스 클래스에서 불러와 사용했습니다.

* @Controller : 브라우저의 URI 를 통해 들어온 사용자의 요청을 받아주는 역할을 하는 클래스에 사용했습니다. HttpServlet 을 상속하여, Http 메소드 요청을 처리할 수 있습니다.

* @Service : 사용자의 요청에 대한 응답을 위한 로직을 담은 클래스에 사용했습니다.

* @Repository : 많이 사용해보지 않아 잘 모르겠습니다.