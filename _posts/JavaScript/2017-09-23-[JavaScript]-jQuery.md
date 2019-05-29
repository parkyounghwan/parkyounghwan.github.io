---
layout: post
title:  "[JavaScript]-jQuery"
date:   2017-09-23 
categories: JavaScript
comments: false
---
자주 사용하는 로직을 재사용할 수 있도록 고안된 소프트웨어를 라이브러리라고 한다.

  


jQuery는 DOM 을 내부에 감추고 보다 쉽게 웹페이지를 조작할 수 있도록 돕는 도구이다.

  


*content delivery network(CDN) : 네트워크 상에 내가 가장 가까이 있는 네트워크에서 컨텐츠 받아오는 것.

  


1. 제어 대상을 찾기(jQuery)

1)

  


$('li').css('color', 'red'); -> <li style="color: red">

  


$(' ') -> jQuery function

li -> css 선택자

  


$()는 jQuery의 함수이다. 이 함수의 인자로 CSS선택자(li)를 전달하면 jQuery 객체라는 것을 리턴한다.

  


**-**TAG

**DOM**

var lis = document.getElementsByTagName('li');

for(var i=0; i<lis.length; i++) {

lis[i].style.color='red';

}

  


**jQuery**

$('li').css('color', 'red');

  


-Class

**DOM**

var lis = document.getElementsByClassName('active');

for(var i=0; i < lis.length; i++) {

lis[i].style.color='red';

}

  


**jQuery**

$('.active').css('color', 'red');

  


-ID

**DOM**

var li = document.getElementById('active');

li.style.color='red';

li.style.textDecoration='underline';

  


**jQuery**

$('#active').css('color', 'red').css('textDecoration', 'underline');

  


active 객체를 리턴하고 chaining (연속적으로) 작업을 진행한다.

  


2) HTML Element

var li = document.getElementById('active');

console.log(li.constructor.name); //HTMLLIElement 

 // 우리가 조회한 객체가 하나라면 HTMLElement

  


var lis = document.getElementsByTagName('li');

console.log(lis.constructor.name); //HTMLCollection

 //조회한 객체가 복수개라면 HTMLCollection

  


3)HTML Collection

