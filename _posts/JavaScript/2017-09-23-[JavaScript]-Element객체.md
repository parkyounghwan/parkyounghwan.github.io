---
layout: post
title:  "[JavaScript]-Element객체"
date:   2017-09-23 
categories: JavaScript
comments: false
---
1. DOM Tree

문서 스크립팅, 자바 스크립트의 핵심, Element를 파악하는 것이 스크립팅 프로그래밍의 핵심이다.

![](https://t1.daumcdn.net/cfile/tistory/99DD053359C62B152D)

  


2. 속성 API

var t = document.getElementById('target');

  


t.getAttribute('id'); //태그의 속성 가져오기

  


t.setAttribute('href', 'http://opentutorials.org/course/1'); //태그에 속성 추가, 변경하기

  


t.removeAttribute('property\_name'); //태그의 속성 지우기

  


t.hasAttribute('title'); //true or false

  


  


a) 속성 vs 프로퍼티

<p id="target">hello world</p>

  


var target = document.getElementById('target');

  


*속성 변경

//attribute 방식

target.setAttribute('class', 'important');

  


//property 방식(변경하는 이름이 조금씩 다르다.)

target.className = 'important';

  


![](https://t1.daumcdn.net/cfile/tistory/991C723359C634662D)

  


3. 식별자 API

엘리먼트를 제어하기 위해서는 그 엘리먼트를 조회하기 위한 식별자가 필요하다. 

HTML에서 엘리먼트의 이름과 id 그리고 class는 식별자로 사용된다. 

  


1) Element.tagName

  


document.getElementById('id\_name or class\_name'').tagName //id, class를 조회해서 태그의 이름을 조회한다.

  


tagName은 읽기 전용.

  


2) Element.id

HTML 문서에서 id는 단 하나만 등장할 수 있는 식별자다. 'Element'.id는 값을 읽고 변경 할 수 있다.

  


//id = "active" 라는 속성을 가진 태그가 있다고 할 때

var active = document.getElementById('active'); //id 값이 active인 태그를 조회하여 active 변수에 넣는다.

  


active.id = 'deactive'; //active의 값을 변경한다.

  


3) Element.class

클래스는 여러개의 엘리먼트를 그룹핑할 때 사용한다. *사용하기 굉장히 까다로워 진보된 classList를 주로 사용한다.

  


//id = "active" 라는 속성을 가진 태그가 있다고 할 때

var active = document.getElementById('active');

  


active.className //class name 확인

  


기존의 클래스 이름에서 이름을 추가할 경우

active.className = active.className + " add classname";

  


*추가 하려면 기존의 클래스 이름이 무엇인지 알아야 하며, 수정하려면 수정하려는 것만 수정하는 것이 아니고 전체를 수정해야 한다.

이런 불편함을 보완하는 것이 class.List

  


*id 와 다르게 class 식별자(프로퍼티)는 className 인데 이는 javascript 예약어와 겹치기 때문이다.

  


4) Element.classList

  


var active = document.getElementById('active');

  


*DOMTokenList 유사 배열 형태로 class가 가지고 있는 모든 class를 보여준다.

ex) class="marked current" //marked 하나 current 하나씩

active.classList[0]; 

=> marked  


  


active.classList.add('important');

=> marked current important

  


active.classList.remove('important');

=> marked current

  


active.classList.toggle('important'); //없으면 생기고 있으면 삭제한다.

=> marked current important

  


active.classList.toggle('important'); 

=> marked current

  


4. 조회 API

문서 전체에서 무언가를 찾을 때는 document를 통해서 메소드를 호출해 사용했다. //document.getElementBy*

document 객체는 문서 전체를 의미하는 엘리먼트 이기 때문에 document의 조회 메소드는 문서 전체를 대상으로 엘리먼트를 조회한다.

element 객체 역시도 getElementBy* 엘리먼트를 가지고 있는데 이 메소드는 해당 엘리먼트의 하위 엘리먼트를 대상으로 조회를 수행한다.

  


var active = document.getElementById('active'); // 문서 전체를 대상으로 엘리먼트 조회.

var list = **active**.getElementsByClassName('marked'); //active 엘리먼트의 하위 엘리먼트에서 marked를 조회한다.

  


  


5. jQuery 속성 제어 API

지금까지 살펴본 Element의 API에 해당하는 기능을 jQuery에서는 어떻게 구사하는가를 알아보자.

  


setAttribute / getAttribute => attr, removeAttribute => removeAttr 로 대체

  


1) attr

  


![](https://t1.daumcdn.net/cfile/tistory/993E923359C7BB622B)

  


 2) attribute 와 property

  


//id 값이 target인 엘리먼트가 있다고 할때

var target = document.getElementById('target');

target.**setAttribute**('class', 'important'); //attribute 방식

target.**className** = 'important'; //property 방식(property를 이용해서 엘리먼트의 속성을 제어하는 방식)

*jQuery에서도 위의 두 방식을 지원한다.

-attr은 attribute 방식

-prop 는 property 방식

  


![](https://t1.daumcdn.net/cfile/tistory/99EE313359C7BDA926)

  


  


*jQuert 내부적으로 html 속성의 원래 이름을 사용하건, 변경된 엘리먼트의 이름을 사용하건 알아서 바꿔 준다.

![](https://t1.daumcdn.net/cfile/tistory/99E2B03359C7BDC230)

  


  


6. jQuery 조회 범위 제한

문서 전체에서 말고 엘리먼트 객체의 하위의 객체를 jQuery에서는 어떻게 조회할까?

  


// id='active'하위에 class='marked' 가 있다고 하자.

$(".marked", "#active").css("background-color", " red"); //id가 active인 엘리먼트의 하위 엘리먼트 중에서 class 가 marked인 엘리먼트에 대해 속성 적용.

  


*간단하게 가자

$("#active .marked").css("background-color", "red"); 

  


*find() 메소드

$('#active').find('.marked').css("background-color", "red"); //active에서 marked 찾기.

  


?쓰임새 비슷한데 find는 언제 쓰냐

![](https://t1.daumcdn.net/cfile/tistory/998CB33359C7C0611A)

  


