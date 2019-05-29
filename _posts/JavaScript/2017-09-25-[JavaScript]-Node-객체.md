---
layout: post
title:  "[JavaScript]-Node-객체"
date:   2017-09-25 
categories: JavaScript
comments: false
---
*Node 객체는 DOM에서 시조와 같은 역할을 한다. 다시 말해서 모든 DOM객체는 Node객체를 상속 받는다.

  


![](https://t1.daumcdn.net/cfile/tistory/99AD003359C7CA9F34)

  


1. Node 관계 API

- Node 객체는 Node 간의 관계 정보를 담고 있는 일련의 API를 가지고 있다.

  


*줄 바꿈 사이에 있는 텍스트도 노드의 객체이다. (body 태그와 ul 태그 사이)

![](https://t1.daumcdn.net/cfile/tistory/9947173359C89A6B38)

  


* **firstChild**는 객체로 받은 태그의 하위 태그를 나타낸다. 위 예제로 보면 변수 s에 body 태그를 담았고,

s.firstChild 를 실행하면 <body>와 <ul> 사이의 **공백(#text)**이 첫번째 하위 객체이다.  


  


*그 하위 객체(태그)의 동일 선상, 동일 깊이에 있는 태그를 검색할 때는 **nextSibling **을 사용한다.  


s.firstChild.nextSibling 은 **<ul>**

s.firstChild.nextSibling.nextSibling 은 </ul> 과 <script> 사이의 **공백**이다.

s.firstChild.nextSibling.nextSibling.nextSibling 은 **<script>**

=> 공백(#text)과 <ul>, <script> 태그는 같은 선상, 동일 깊이에 있는 태그들이다.

  


*childNodes, 하위 선상의 노드들의 집합  


  


*parentNode, 상위 노드

  


2. 노드 종류 API  


  


-nodeType : 노드의 타입이 텍스트인지 엘리먼트 인지 Document인지 알려준다.

-nodeName : 노드의 이름이나 태그의 이름을 알려준다.

  


![](https://t1.daumcdn.net/cfile/tistory/99E89B3359C8A75E15)

  


*엘리먼트.nodeType 으로 검색 가능하며 보라색 숫자는 타입을 나타내는 상수.

  


2-1) 재귀함수 

-재귀 함수를 통해 원하는 태그를 뽑아낸다.

  


*html 코드는 위에 '노드 객체 API'와 같음.

  


**=> 1단계 : traverse 라는 함수로 원하는 태그의 위치를 찾아낸다.**

-traverse라는 function(함수)를 짰고, 그 밑에서 traverse에 매개변수를 넣어 실행 시킨다. 

![](https://t1.daumcdn.net/cfile/tistory/9989D73359CC7D9320)

  


(요런 느낌)

![](https://t1.daumcdn.net/cfile/tistory/997C523359CC7EB713)

  


*출력결과

![](https://t1.daumcdn.net/cfile/tistory/99BC8E3359CC7EFD18)

  


  


**=> 2단계 : 재귀함수를 통해 target 이하의 태그들을 모두 출력한다.**

![](https://t1.daumcdn.net/cfile/tistory/99DF7E3359D3346906)

**  
**

**  
**

***** target에 담겨있는 하위 노드를 c에 할당 (#text, ul, #text, script, #text)

  


  


  


  


  


  


  


  


**=> 3단계 : #text를 제외한 ElementNode 만 뽑아낸다.**

![](https://t1.daumcdn.net/cfile/tistory/9904153359D339772E)

**  
**

**  
**

**=> 4단계 : a tag만 추출**

![](https://t1.daumcdn.net/cfile/tistory/994CEB3359D339F60F)

**  
**

**  
**

**=> 결과**

![](https://t1.daumcdn.net/cfile/tistory/9960BF3359D33A1F32)

  


