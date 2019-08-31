---
layout: post
title: "Java, Optional"
date:   2019-08-31
categories: Java
comments: false
---

* https://www.daleseo.com/java8-optional-after/ 해당 블로그 내용 정리
* NulPointerExpcetion
* 함수형 언어에서의 'null' 처리
* Optional
* Stream 처럼 사용하기
* Java 8 이전의 코드를 Optional 하게 바꾸기
* *ifPresent()*



<br/>

## NullPointerException

* 지뢰같다. 
* 컴파일 타임에는 조용히 있다가, 런타임 시에 터져나온다.
* 'NPE' 방어를 위해 코드 사이 사이에 녹아있는 'null' 체크 로직 때문에, 코드 가독성과 유지 보수성이 떨어진다.

<br/>

## 함수형 언어에서의 'null' 처리

스칼라나 히스켈 같은 함수형 언어에서는 전혀 다른 방법으로 '존재하지 않는 값'을 표현한다.

* '존재 할지 안 할지 모르는 값'을 표현할 수 있는 별개의 타입을 갖는다.
* 위 타입의 값을 제어 할 수 있는 여러가지 API 를 제공한다.
* 함수형 언어의 영감을 받아 Java 8 에서 'Optional' 클래스 도입

<br/>

## Optional

### Optional 이란?

* 존재 할 수도 있지만, 안 할 수도 있는 객체
* 'null' 이 될 수도 있는 객체를 감싸고 있는 'Rapper' 클래스
* 원소가 없거나, 하나 밖에 없는 'Collection' 이나 'Stream' 의 형태로 생각.
* 'null' 을 담는 특수한 그릇.

### Optional 의 효과

* 'null' 체크를 직접 하지 않아도 된다.
* 명시적으로 해당 변수가 'null' 일 수도 있다는 가능성을 표현할 수 있다.

### Optional 객체 생성하기

Optional 클래스는 간편하게 객체 생성을 할 수 있도록, 3가지 정적 팩토리 메서드를 제공한다.

* Optional.empty()
  *'null' 을 담고 있는, 비어있는 Optional 객체를 얻어옴*

  ~~~java
  Optional<T> maybeTClass = Optional.empty();
  ~~~

  * 'null' 일 경우 비어있는 Optional 객체를 반환

  

* Optional.of(value)
  *'null' 이 아닌 객체를 담고 있는 Optional 객체 생성*

  ~~~java
  Optional<T> maybeTClass = Optional.of(new TClass);
  ~~~

  * 'null' 이 넘어올 경우, NPE 를 던지기 때문에 주의해서 사용.

  

* Optional.ofNullable(value)
  *'null' 인지 아닌지 확신 할 수 없는 객체를 담고 있는 Optional 객체를 생성*

  ~~~java
  Optional<T> maybeTClass = Optional.ofNullable(new TClass);
  Optional<T> maybeNotTClass = Optional.ofNullable(null);
  ~~~

  * 'empty()' 와 'of()' 를 합쳐 놓은 메소드
  * 'null' 이 넘어올 경우 NPE 를 던지지 않고, 비어있는 Optional 객체를 반환

### Optional 이 담고 있는 객체 접근하기

Optional 클래스는 담고 있는 객체를 꺼내오기 위해 다양한 인스턴스 메서드를 제공.

아래 메서드들은 모두 Optional 이 담고 있는 객체가 존재할 경우 동일하게 해당 값을 반환.

반면에, 비어있는 경우(null)에 다르게 동작한다. 

다르게 동작하는 부분을 설명하겠다.

* *get ()*
  * 'NoSuchElementException' 발생
* *orElse (T other)*
  * 넘어 온 인자 반환
* *orElseGet (Supplier<? extends T> other)*
  * 넘어 온 함수형 인자를 통해서 생성된 객체를 반환
  * 비어있는 경우에만 함수가 호출
* *orElseThrow (Supplier<? extends X> exceptionSupplier)*
  * 넘어 온 함수형 인자를 통해서 생성된 예외를 던짐

### Optional 의 잘못된 사용

위의 *get()* 의 경우 비어있는 객체를 대상으로 호출할 경우, 예외를 발생시키므로 'null' 체크가 필요하다.

~~~java
String text = getText();
Optional<String> maybeText = Optional.ofNullable(text);
int length;
if (maybeText.isPresent()) {
	length = maybeText.get().length();
} else {
	length = 0;
}
~~~

같은 코드를 Optional 없이

~~~java
String text = getText();
int length;
if (text != null) {
	length = maybeText.get().length();
} else {
	length = 0;
}
~~~

위 코드를 보면 Optional 을 사용하지 않는 편이 더 낫다. 잘못된 사용법이다.

안타깝게도 많은 개발자들이 **Optional 적용 후 어떻게 null 체크를 해야 하나요?** 라는 질문을 하게 된다.

우리가 Optional 을 사용하는 이유는 **고통스러운 null 처리를 직접하지 않고 Optional 클래스에 위임하기 위함** 이다.

'Optional' 을 정확히 이해하고 사용하려면 다음과 같이 한줄의 코드로 작성할 수 있어야 한다.

~~~java
int length = Optional.ofNullable(getText()).map(String::length).orElse(0);
~~~

<br/>

## Stream 처럼 사용하기

Optional 을 제대로 사용하려면, Optional 을 **최대 1개의 원소를 가지고 있는 특별한 Stream** 이라고 생각하면 좋다.

Optional 클래스는 Stream 클래스와 직접적인 구현이나 상속 관계는 없지만 사용 방법이나 기본 사상이 매우 유사하다.

Stream 클래스가 가지고 있는 *map()* 이나 *flatMap()*, *filter()* 와 같은 메서드를 Optional 도 가지고 있다.

### *map()* 으로 변신하기

예제를 다시 보면서, 단계별로 짚어 보자.

~~~java
int length = Optional.ofNullable(getText()).map(String::length).orElse(0);
~~~

* *ofNullable()* 로 Optional 객체를 정적 팩토리 메서드를 호출하여 String 객체를 Optional 로 감싸주었다.
* String 객체가 null 을 반환할 경우를 대비하여, *of()* 대신에 *ofNullable()* 을 사용함.
* *map()* 을 통해 Optional 에 담긴 객체 타입을 바꿔주었다.
* *orElse()* 를 호출하여 Optional 이 비어있을 경우 디폴트로 사용할 값(0)을 세팅해주었다. 



### filter() 로 레벨업

Java 8 이전에 NPE 방지를 위해 null 체크로 시작하는 if 조건문 패턴을 자주 보았을 거다.

~~~java
if (obj != null && obj.do() ...) { ... }
~~~

예를들어,

> 주어진 시간(분) 내에 생성된 주문을 한 경우에만 해당 회원 정보를 구하라

는 메서드를 위 패턴으로 작성해 본다면

~~~java
public Member getMemberIfOrderWithin (Order order, int min) {
  if (order != null && 
      (order.getDate().getTime() > System.currentTimeMillis() - (min * 1000) {
        return order.getMember();
      }
}
~~~

위 코드는 일단

* 가독성이 떨어진다.
* null 을 리턴할 수 있기 때문에 메서드 호출부에 NPE 위험을 전파 (*'getDate()'*, *'getTime()'*)

위 코드를 *filter()* 를 사용하면

~~~java
public Optional<Member> getMemberIfOrderWithin(Order order, int min) {
  return Optional.ofNullable(order)
    						.filter(o -> o.getDate().getTime() > System.currentTimeMillis() - (min * 1000))
    						.map(Order::getMember);
}
~~~

* 읽기 편함
* 메소드의 리턴 타입을 Optional 로 사용함으로써 호출자에게 해당 메서드가 null 을 담고 있는 Optional 객체를 반환 할 수도 있다는 것을 명시적으로 알림
* *filter()* 메서드는 넘어온 함수형 인자의 리턴 값이 false 인 경우, Optional 을 비워버리므로 그 이후의 메서드 호출은 의미가 없음.

<br/>

## Java 8 이전의 코드를 Optional 하게 바꾸기

### 1. null 반환

**Map** 인터페이스의 *get()* 메소드는 주어진 인덱스에 해당하는 값이 없으면 null 을 반환한다.

~~~java
Map<Integer, String> cities = new HashMap<>();
cities.put(1, "Seoul");
cities.put(2, "Inchone");
cities.put(3, "Busan");
~~~

따라서 해당 API 를 사용하는 코드는 'null-safe' 하게 만들기 위해 null 체크를 해줘야 한다.

~~~java
String city = cities.get(4);	// return null
int length = ((city == null) ? 0 : city.length());	// null check

System.out.println(length);
~~~

*get()* 의 반환값을 Optional 로 감싸주면, 자연스럽게 'null-safe' 한 코드가 된다.

~~~java
Optional<String> maybeCity = Optional.ofNullable(cities.get(4));	// Optional
int length = maybeCity.map(String::length).orElse(0);	// null-safe

System.out.println("length: " + length);
~~~



### 2. 예외 발생

**List** 인터페이스의 *get()* 은 주어진 인덱스에 해당하는 값이 없으면 'ArrayIndexOutOfBoundsException' 을 던진다.

~~~java
List<String> cities = Arrays.asList("Seoul", "Inchone", "Busan");
~~~

따라서, 다음과 같이 *try-catch* 구문을 사용하여 예외 처리를 해줘야 한다.

예외처리 후에도 null-check 도 해줘야 해서, 코드가 지저분해 진다.

~~~java
String city = null;

try {
  city = cities.get(3);	// throws exception
} catch (ArrayIndexOutOfBoundsException e) {
  ...
}

int length = ((city == null) ? 0 : city.length());

System.out.println(length);
~~~

이런 경우, 다음과 같이 예외 처리부를 감싸서 **정적 유틸리티 메소드** 로 분리해주면 좋다.

~~~java
public static <T> Optional<T> getAsOptional(List<T> list, int index) {
  try {
    return Optional.of(list.get(index));
  } catch (ArrayIndexOutOfBoundsException e) {
    return Optional.empty();
  }
}

...OtherClass

Optional<String> maybeCity = getAsOptional(cities, 3);	// Optional
int length = maybeCity.map(String::length).orElse(0);	// null-safe
System.out.println("length: " + length);
~~~

* Optional 클래스의 정적 팩토리 메서드를 사용해, 정상 처리 시 와 예외 처리 시 에 반환할 Optional 객체를 각각 지정해 줌.
* 이 경우에는 Optional 에 담을 객체가 null 인지 아닌지 확실히 알 수 있어, *Optional.ofNullable()* 대신에 다른 2개의 정적 팩토리 메소드를 사용.

<br/>

## *ifPresent()*

* *ifPresent(Consumer<? super T> consumer)*
  * 특정 결과를 반환하는 대신, Optional 객체가 감싸고 있는 값이 존재할 경우에만 실행될 로직을 함수형 인자로 넘길 수 있다.
  * 함수형 인자로 람다식이나 메소드 레퍼런스가 넘어올 수 있다.
  * 비동기 메소드의 콜백 함수 처럼 작동.

~~~java
Optional<String> maybeCity = getAsOptional(cities, 3);	// Optional
maybeCity.ifPresent(city -> {
  System.out.println("length: " + city.length());
});
~~~

