---
layout: post
title: "Generic"
date:   2019-07-08
categories: Java
comments: false
---

여러가지 자료형을 허용하고 싶을 때 Object 로 선언 할 수 있지만, 그렇게 하면 원하지 않는 자료형이 입력 되었을 때, 오류를 컴파일 시점에 잡아 낼 수 없게 된다.  

제네릭은 jdk1.5 버전 부터 사용할 수 있다. 제네릭을 지원하기 전에는 컬렉션에서 객체를 꺼낼 때 마다 형변환을 해야 했다. 1.5 부터는 제네릭을 사용하면 컬렉션에 담을 수 있는 타입을 컴파일러에게 알려주며, 컴파일러가 알아서 형변환 코드를 추가한다. 또한 엉뚱한 객체를 넣는 코드가 있다면 컴파일 시점에 차단해 준다.  

~~~java
List<String> list = new ArrayList<>();

list.add(1);	// error
list.add("str");
~~~

<br/>

**제네릭은 클래스 내부에서 사용할 데이터 타입을 외부에서 지정하는 기법**

<br/>

제네릭을 사용하여 개발하는 시점은 총 3가지 경우가 있다.

* Class
* Method
* Interface

제네릭을 구현하는 세가지 방식에 대해 알아보고, 제네릭을 사용하는 이유와 _extends_ 에 대해 알아보자.

<br/>

### Generic Class

---

클래스 **내부** 에서 사용될 자료형을 지정 하는 것. 대표적인 예로, ArrayList 가 있다.

~~~java
class Foo <T> {
  private T t;
  
  public void set (T t) {
    this.t = t;
  }
  
  public T get () {
    return t;
  }
}

// 사용 시
Foo <String> f1 = new Foo <String> ();
Foo <Integer> f2 = new Foo <Integer> ();
~~~

* 위 처럼 클래스 **내부** 에서 사용 될 타입을 사용 시점 (**외부**) 에서 지정해 줄 수 있다.
* 즉, 클래스를 정의 할 때, 데이터 타입을 확정하지 않고 인스턴스를 생성할 때, 데이터 타입을 지정하는 기능이 제네릭.

<br/>

### Generic Method

---

클래스에 제네릭을 선언하지 않고, 메소드에만 선언하는 방법. 주의 할 점은, 파라미터 타입 또는 리턴 타입에 제네릭을 선언했으면, **메소드의 리턴 타입 앞에도 똑같이 선언** 해 주어야 한다.

~~~java
// 파라미터의 타입 'T' 이니까 메소드의 리턴 타입 앞에 똑같이 선언.
public <T> void method1 (T t) { ... }	

// 사용 시
Foo foo = new Foo();

String str = "str";
foo.<String>method1(str);

// 리턴 타입이 Generic Class 이므로, 앞에 제네릭 타입 선언.
public <T> Foo<T> method2 (T t) {	
  return new Foo<>();
}
~~~

<br/>

### Generic Interface

---

제네릭 클래스와 비슷하며, 조금 더 유연한 구현(implements)이 가능하다.

~~~java
// 타입 매개변수를 선언하는 부분이 추가된 것을 빼면, 일반적인 인터페이스와 동일하다.
public interface Koo <T> {
  public T method3(T t);
}

class Roo<T> implements Koo<T> {
  @Override
  public T method3(T t) { ... }
}  

// 사용 시
Roo<Integer> roo1 = new Roo<>();
Roo<String> roo2 = new Roo<>();

roo1.method(1);	// ok
roo2.method("str");	// ok
~~~



* 구현 시, 제네릭 클레스로 구현하지 않으면 에러가 생길 수 밖에 없다.
* _Koo_ 인터페이스 에는 제네릭 메소드가 있어서, 클래스 안에서 T 타입을 사용 할 수 없으니, 동일하게 제네릭 형 매개변수를 맞추는 것.
* 사용 시, _Roo_ 클래스의 실제 타입 인 Integer 와 String 을 전달해서, 선언 한 _Roo_ 클래스의 타입을 설정해 줌.

<br/>

### 제네릭을 사용하는 이유

---

* [생활코딩 - 제네릭(Generic)](https://opentutorials.org/module/516/6237) 에 정말 잘 나와 있다.

<br/>

결론부터 말하자면, **타입 안전성** 을 위해서 사용한다. 어떤 특정 클래스의 파라미터를 _Object_ 타입으로 받는다고 생각해보자.  

_Object_ 는 어떤 타입이든 다 받아들일 수 있다. 따라서 컴파일 시에는 문제가 없지만, 클래스 내부적으로 원하는 타입이 아닐 경우, 런타임 시 에러를 발생 시킨다.

~~~java
class StudentInfo {
  public int age;
  
  public StudentInfo (int age) {
    this.age = age;
  }
}

class Person {
  public Object info;
  
  public Person (Object info) {
    this.info = info;
  }
}

// 사용 시
Person person1 = new Person("yhpark");
StudentInfo si = (StudentInfo) person1.info;
~~~

* Person 의 생성자는 매개변수 info 의 데이터 타입이 Object 이며, 모든 객체가 될 수 있다. 때문에 StudentInfo 의 객체가 아니라 String 이 와도 컴파일 시에 에러가 발생하지 않는다.

<br/>

### extends, 와일드 카드

---

#### extends

제네릭으로 올 수 있는 데이터 타입을 특정 클래스의 자식으로 제한 할 수 있다.  

타입을 제한하는 용법은 **< T {extends or super} {class or interface}>** 의 형태로 쓰인다.

> 상위 타입이거나 상위 타입의 하위 클래스 또는 구현 클래스만 허용하겠다.

예를들어, _extends_ 로 Number 클래스를 설정하면, 하위 클래스 (Byte, Short, Integer, Long, Double) 를 허용한다.

* <T extends String> : 클래스 String 자신 또는 String 을 상속하는 아무 타입.
* <T extends List> : 클래스 List 자신 또는 List 를 상속하는 아무 타입.
* <T super HashMap> : 클래스 HashMap 자신 또는 HashMap 이 상속하는 아무 타입.

<br/>

#### 와일드 카드

https://palpit.tistory.com/668