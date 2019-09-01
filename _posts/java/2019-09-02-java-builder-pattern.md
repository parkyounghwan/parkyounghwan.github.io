---
layout: post
title: "Java, Buidler Pattern"
date:   2019-09-02
categories: Java
comments: false
---

* [객체 생성을 깔끔하게](https://johngrib.github.io/wiki/builder-pattern/)

  > 상기 블로그를 참고함, 블로그 내용 중 *Effective Java* 의 내용만 흡수

<br/>

## 객체 생성을 깔끔하게

### 점층적 생성자 패턴

- 필수 인자를 받는 *필수 생성자* 를 하나 만든다.

  1. 1 개의 선택적 인자를 받는 생성자를 추가한다.
  2. 2 개의 선택적 인자를 받는 생성자를 추가한다.
  3. n 개의 선택적 인자를 받는 생성자를 추가한다.
  4. 모든 선택적 인자를 다 받는 생성자를 추가한다.
  5. (모든 선택적 인자를 다 받는 생성자를 먼저 만들지 않으면, IDE 상에서 오류가 발생함, 다른 생성자를 만들 때, 기본적으로 모든 인자를 포함한 생성자를 먼저 만들어 줘야 한다.)

  

  ```java
  public class Member {
    private final String name;			// 필수 인자
    private final String location;	// 선택적 인자
    private final String hobby;			// 선택적 인자
    
    // 모든 선택적 인자를 다 받는 생성자
    public Member (String name , String location, String hobby) {
      this.name = name;
      this.location = location;
      this.hobby = hobby;
    }
    
    // 필수 생성자
    public Member (String name) {
      this (name, "출신 지역 비공개", "취미 비공개");
    }
    
    // 1 개의 선택적 인자를 받는 생성자
    public Member (String name, String location) {
      this (name, location, "취미 비공개");
    }
  }
  ```

  - *'new Member("홍길동", "출신 지역 비공개", "취미 비공개")'* 같은 호출이 빈번하게 일어난다면, ***'new Member("홍길동")'*** 으로 대체 할 수 있다.
  - 다른 생성자를 호출하는 생성자가 많아져, 인자가 추가되는 일이 발생하면 코드를 수정하기 어렵다. (위 'Member' 클래스에 'age' 필드가 들어가면 만들어 놓은 생성자 전체를 수정해 주어야 함)

  > *this ( ... )*
  >
  > - 클래스에 오버로딩 된 다른 생성자를 호출한다.
  > - 생성자의 최상단에 사용되어야 한다.
  > - 하나의 클래스에 여러개의 생성자가 오버로딩 되어 있을 때, 일부분을 제외하고 서로 중복된 코드를 가지고 있는 경우가 많을 때 사용.

  

<br/>

### 자바빈 패턴

위 *점층적 생성자 패턴* 의 대안.

**이 패턴은 *setter* 메서드를 이용해 생성 코드를 읽기 좋게 만드는 것**

~~~java
Member member = new Member();
member.setName("yhpark");
member.setLocation("출신 지역 비공개");
member.setHobby("취미 비공개");
~~~

* 장점
  * 각 인자의 의미를 파악하기 쉬움.
  * 복잡하게 생성자를 여러개 만들지 않아도 된다.
* 단점
  * 객체 일관성이 깨진다.
    * 1회의 호출로 객체 생성이 끝나지 않음 (1합에 생성하지 않고 생성한 객체에 값을 계속 붙여나가는 형태)
  * *setter* 메서드가 있으므로 변경 불가능(immutable) 클래스를 만들 수 없다.
    * 스레드 안전성을 확보하려면 점층적 생성자 패턴보다 많은 일을 해야 한다.

<br/>

### 빌더 패턴

* Builder Pattern 으로 생성한 Entity

  ~~~java
  public class Member {
    private final String name;
    private final String location;
    private final String hobby;
    
    public static class Builder {
      // 필수 인자 (Required Parameters)
      private final String name;
      
      // 선택적 인자 (Optional Parameters) - 선택적 인자는 기본값으로 초기화
      private String location = "출신 지역 비공개";
      private String hobby = "취미 비공개";
      
      public Builder (String name) {
        this.name = name;
      }
      
      public Builder location (String loc) {
        location = loc;
        return this;			// 이렇게 하면 '.' 으로 체인을 이어갈 수 있다.
      }
      
      public Builder hobby (String hob) {
        hobby = hob;
        return this;
      }
      
      public Member build() {
        return new Member(this);
      }
    }
    
    private Member (Builder builder) {
      name 		 = builder.name;
      location = builder.location;
      hobby 	 = builder.hobby;
    }
  }
  ~~~

  > *this*
  >
  > * 객체 자신의 참조값을 전달하고 싶을 때
  > * 어떤 메서드에서 동작을 완료하고 리턴값으로 자기 자신의 참조값을 전달하고 싶을 때

* 객체 호출

  ~~~java
  // Builder 생성
  Member.Builder builder = new Member.Builder("yhpark");
  builder.location("Seoul");
  builder.hobby("exercise");
  
  // Member 객체 생성
  Member member = builder.build();
  ~~~

  또는

  ~~~java
  Member member = new Member
  	.Builder("yhpark")		// 필수값 입력
  	.location("Seoul")
  	.hobby("exercise")
  	.build();							// build() 가 객체를 생성해 돌려준다. 
  ~~~

  * 장점
    * 각 인자가 어떤 의미인지 알기 쉽다.
    * *setter* 메소드가 없으므로 변경 불가능한 객체를 만들 수 있다.
    * 한 번에 객체를 생성할 수 있으므로, 객체 일관성이 깨지지 않는다.
    * *build* 메서드로 잘못된 값이 입력되었는지 검증하게 할 수도 있다.



