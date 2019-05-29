---
layout: post
title:  "[JavaScript]-DOM"
date:   2017-09-21 
categories: JavaScript
comments: false
---
문서를 자바스크립트로 제어하려면 제어하려는 대상 객체를 문서에서 찾아내야 한다.

  


document.getElementsByClassName

  


document는 문서 전체를 의미하는 객체(hmtl 문서)

  


getElementsByTagName('태그명');

  


  


 렌더링 엔진은 HTML 문서를 파싱하고 콘텐츠 트리 내부에서 태그를 DOM 노드로 변환한다.

 - 문서 파싱은 브라우저가 코드를 이해하고 사용할 수 있는 구조로 변환하는 것을 의미

 - 파싱 결과는 보통 문서 구조를 나타내는 노드 트리인데 파싱 트리 또는 문법 트리라고 부른다.

 - 파싱은 문서에 작성된 언어 또는 형식의 규칙에 따르는데 파싱할 수 있는 모든 형식은 정해진 용어와 구문 규칙에 따라야 한다. 이것을 문맥 자유 문법이라고 한다. 

 - 파싱 vs 컴파일

 파싱 = 분리, 해석 -> 컴파일러가 소스파일을 실행가능한 형태로 번역하기 전에 소스파일을 의미있는 단어의 단위로 잘라서 해석하는 작업(ex. printf(“hello”) -> printf, (, ”, hello, “, ) )

 컴파일 = 번역 -> 프로그래밍 언어로 되어있는 소스파일을 컴퓨터가 실행가능한 기계어로 바꾸는 작업. 소스파일(텍스트파일)을 바이너리 파일로 바꿔준다.

 문서(document)란 HTML이나 XML문서와 같이 부분적 요소나 내용이 관련된 것들끼리 묶여서 존재하는 구조화된 문서입니다.(ex. 같은 내용은 같은 태그안에 존재), 이렇게 구조화 된 문서에 스크립트를 이용하여 접근할 때에도, **구조적으로**** ****표현하는**** ****방식****(Object Model)****을**** ****제공하는**** ****것이**** ****바로**** DOM****이라고**** ****보면**** ****됩니다****.**

  


 각 element를 트리의 node로 표현하는 DOM트리를 통해 이를 쉽게 알 수 있습니다. (원래 DOM은 DNM:Document Node Model이었는데 이름부르기 어렵다고 바뀜)

  


![](https://t1.daumcdn.net/cfile/tistory/99AB0A335A0ACD8A13)

  


  


 위 트리 구조를 보면, Element뿐만 아니라 Attribute, Text까지 노드로 표현되어 있음을 알 수 있습니다. **즉**** DOM****을**** ****통해**** ****스크립트가**** ****문서**** ****내의**** ****모든**** ****요소에**** ****동적으로**** ****접근할**** ****수**** ****있다는**** ****것입니다****. **그래서 DOM을 사용하면 문서상의 요소에 접근해 생김새나 내용, 속성을 조작 할 수 있습니다. 이러한 점 때문에 DOM접근은 웹 페이지 상의 풍부한 상호작요을 위해서 꼭 필요한 작업 중에 하나입니다.

  


 하지만 이를 순수 JavaScript로 하게 되면, 다수의 반복문과 긴 스크립트를 작성해야 하는 경우가 많습니다. 바로 이 문제를 해결하는 것이 jQuery의 장점 중 하나 입니다.

  


 jQuery에서는 CSS의 선택자 방식을 사용해서 DOM에 접근합니다.

  


 jQuery에서는 jQuery DOM 객체 생성함수인 $(); 을 사용하여 선택자로 간단하게 DOM에 접근한다. 하지만 JavaScript에서는 브라우저의 여러가지 내장 메소드를 통해 DOM에 접근합니다.

  


![](https://t1.daumcdn.net/cfile/tistory/99BB0A335A0ACDBC12)

  


 jQuery를 사용하면, 아무래도 순수 JavaScript에 비해 속도가 느린 것이 사실입니다. 물론 DOM접근 자체를 최소화하는 것이 성능 면에서는 가장 좋은 것이지요. 하지만 단순하면서도 다양한 기능들을 사용할 수 있게 해주는 편리함은, jQuery를 가장 널리 쓰이는 JavaScript라이브러리로 만들어 주었다.

  


 jQuery는 내부적으로 가능하다면 순수 JavaScript의 브라우저 내장 메소드를 사용하게 됩니다. 바로 속도 향상을 위해서 인데요. 하지만 브라우저 내장 메소드가 지원되지 않는 경우, 모든 DOM노드를 순회해야 하기 때문에 속도가 느려집니다.

  


  


  


  


  


  


*hover는 자바스크립트인가?

  


 selector:pseudo-class {

  property: value;

  p.p1 {margin: 0.0px 0.0px 0.0px 0.0px; font: 12.0px '.Apple SD Gothic NeoI'; color: #454545} p.p2 {margin: 0.0px 0.0px 0.0px 0.0px; font: 12.0px 'Helvetica Neue'; color: #454545} p.p3 {margin: 0.0px 0.0px 0.0px 0.0px; font: 12.0px 'Helvetica Neue'; color: #454545; min-height: 14.0px} p.p4 {margin: 0.0px 0.0px 0.0px 0.0px; font: 12.0px '.Apple SD Gothic NeoI'; color: #454545; min-height: 12.0px} li.li1 {margin: 0.0px 0.0px 0.0px 0.0px; font: 12.0px '.Apple SD Gothic NeoI'; color: #454545} li.li2 {margin: 0.0px 0.0px 0.0px 0.0px; font: 12.0px 'Helvetica Neue'; color: #454545} span.s1 {font: 12.0px 'Helvetica Neue'} span.s2 {font: 12.0px '.Apple SD Gothic NeoI'} span.Apple-tab-span {white-space:pre} ol.ol1 {list-style-type: decimal} ul.ul1 {list-style-type: hyphen}  

 }

  


