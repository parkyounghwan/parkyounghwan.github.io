---
layout: post
title: "자바스크립트 클래스"
date:   2019-07-04
categories: Javascript
comments: false
---

### Classes

---

#### 클래스 선언식

ES6 클래스는 생성자와 상속 관계를 좀 더 명확히 보여주는 역할을 한다.

~~~javascript
// ES6
class Student {
  constructor (name) {
    this.name = name;
  }
}

const stu1 = new Student('yhpark');
~~~

클래스는 함수로 취급하며, 내부적으로 클래스명은 _함수명_ 으로, constructor 메소드 바디는 _함수 바디_ 로 간주한다.

~~~javascript
// ES5
function Student (name) {
  this.name = name;
}
~~~

클래스는 함수라고 생각하면 되고, 함수를 생성하는 신상 구문 (ES6) 라고 생각하면 된다.

<br/>

#### 클래스 표현식

클래스 선언과 비슷하지만, 클래스명은 생략 가능하며, 클래스 바디와 로직 구현은 어느쪽이든 같다.

~~~javascript
// ES6
var Student = class {
  constructor (name) {
    this.name = name;
  }
}

const stu1 = new Student('yhpark');
~~~

클래스 참조값을 변수(_Student_)에 할당 후 객체 생성 시 사용하는 구조.

함수로 작성하면 아래와 같다.

~~~javascript
// ES5
const Student = function (name) {
  this.name = name;
}
~~~

<br/>

### 프로토 타입 메소드

클래스 바디( '{…}' ) 안에 있는 메소드는 모두 클래스의 prototype 프로퍼티에 추가된다. 

~~~javascript
// ES6
class Person {
  constructor (name, age) {
    this.name = name;
    this.age = age;
  }
  
  printProfile () {
    console.log('이름: ' + this.name + ', 나이: ' + this.age);
  }
}

const person1 = new Person('yhpark', 29);
person1.printProfile();		// 이름: yhpark, 나이: 29

// 클래스의 함수가 prototype 프로퍼티에 추가되어 있는지 확인
console.log('printProfile' in p.__proto__);				// true
console.log('printProfile' in Person.prototype);	// true

~~~

클래스의 prototype 프로퍼티에 _printProfile_ 메소드가 포함된 걸 확인 할 수 있다.

아래는 함수 버전으로 바꾼 클래스 바디의 메소드 선언.

~~~javascript
// ES6
function Person (name, age) {
  this.name = name;
  this.age = age;
}

// 클래스명.prototype.함수명
Person.prototype.printProfile = function () {
  console.log('이름: ' + this.name + ', 나이: ' + this.age);
}

// 객체 생성과 확인 작업은 위와 동일
~~~

<br/>

#### get/set 메소드

ES5 이전엔 접근자 프로퍼티를 객체에 추가하는 방법은 Object.defineProperty() 분이었다. ES6 부터는 메소드 앞에 get, set 을 붙일 수 있고, 객체 리터럴 또는 클래스에 추가하여 접근자 프로퍼티의 get/set 속성을 정의 할 수 있다.

~~~javascript
// ES6
class Person {
  construtor (name) {
    this._name_ = name;		// js 에는 접근 지시자가 없기 때문에, 클래스 스코프 영역을 구분하기 위한 목적으로 언더 바 사용.
  }
  
  get name () {
    return this._name_;
  }
  
  set name (name) {
    this._name_ = name;
  }
}

const person1 = new Person('yhpark');
person1.name = 'parkyounghwan';

console.log(Object.getOwnPropertyDescriptor(person1.__proto__, 'name'). set);		// function name(name) {this._name_ = name;}
console.log(Object.getOwnPropertyDescriptor(Person.prototype,'name').set)		// function name() {return this._name_;}
~~~

* [코드의 변수나 함수 등에 언더바를 사용하는 이유](https://webisfree.com/2017-11-06/코드의-변수나-함수-등에-언더바를-사용하는-이유는)

  

### 프로퍼티

---

객체에 속한 데이터를 프로퍼티 라고 한다.

~~~javascript
let person = {			// 객체 리터럴
  name: 'yhpark',		// 프로퍼티
  age: 29,
  job: 'student',
};
~~~

_person_ 객체 내부에 위 값들이 모두 저장된 것 같지만, 사실 **name, age, job** 은 모두 값 (data) 들이 저장된 메모리 위치를 가리킬 뿐이다.

따라서, 프로퍼티에 저장된 값 (data) 의 수정 변경 등은 모두 프로퍼티가 가리키는 메모리 위치에서 이루어 지는 일이다.

<br/>

우리가 흔히 메소드(method) 라고 부르는 항목은, 객체 내부에서 프로퍼티로 선언된 함수(function) 을 뜻한다. '함수도 프로퍼티 다'.

<br/>

#### 종류와 속성

프로퍼티는 **데이터 프로퍼티** 와 **접근 프로퍼티**, 2가지 종류로 나뉜다.

또한 프로퍼티는 4가지 속성으로 이루어져 있고, **데이터 프로퍼티**, **접근 프로퍼티** 에 공통된 2가지 속성과 서로 다른 2가지 속성을 가지고 있다.

하나 하나 뜯어보자.

<br/>

#### 데이터 프로퍼티

저장 된 값(data) 에 관련된 프로퍼티 이며, **'Configurable' / 'Enumerable' / 'Writable' / 'Value'**, 의 네 가지 속성이 있다.

* [자바스크립트 객체(Object)의 프로퍼티(Property)와 속성(Property Attribute)](https://muckycode.blogspot.com/2015/04/javascript-object-property-property.html)

  