---
layout: post
title:  "[JavaScript]BOM"
date:   2017-09-21 
categories: JavaScript
comments: false
---
전역변수 : window라는 객체의 프로퍼티(속성)을 만드는 것, 메소드를 만드는 것.

전역객체 = window

  


window - DOM, BOM, JavaScript 이 세가지가 window객체에 소속되어 있다.

  


  


  


-alert(경고창)

함수가 끝나기 전까지는 진행되지 않는다.

  


-confirm(확인)

확인, 취소 버튼 등장

확인 누르면 true 객체 전달, 취소는 false

  


function func\_confirm(){

if(confirm('ok?')){

alert('ok');

} else {

alert('cencel');

}

}

  


-prompt

사용자가 입력한 값을 자바스크립트를 통해 전달.

  


2) Location 객체

window의 문서 URL을 변경 혹은 알아 낼 수 있다.

console.log(location.toString(), location.href);

  


console.log(location);

  


alert(location);

  


URL Parsing

console.log(location.protocol1); -> http:

  


console.log(location.protocol); -> http: or https:

  


console.log(location.host); -> 

*host 각 컴퓨터를 식별하는 주소

  


console.log(location.port);

*서버 컴퓨터에 설치되어 있는 여러 애플리케이션 식별

  


console.log(location.path);

*우리가 찾은 서버 애플리케이션의 특정 정보를 알고 싶다.

  


console.log(location.search);

*우리가 서버에 전달하려는 특정한 값

  


console.log(location.hash);

*그 애플리케이션(홈페이지)의 위치

  


2-1) Location - URL값을 변경해주기도 한다.

 location.href = 'url'; //redirection, 현재 웹페이지가 다른 웹페이지로 이동한다.

  


 location.href = location.href //reload

 location.reload();

  


3) Navigator - 브라우저의 정보를 제공하는 객체, 브라우저에 맞게 설정하기 위함.

브라우저마다 다르게 동작하는 문제, 크로스브라우징 문제

  


console.dir(navigator); //navigator 객체의 모든 프로퍼티를 알 수 있다.

  


console.dir(navigator.appName); //웹브라우져의 이름

  


console.dir(navigator.appVersion); //웹브라우저의 특성

  


userAgent //브라우저가 서버측으로 전송하는 정보(네트워크 접근할때)

  


platform //브라우저가 사용하는 운영체체에 대한 정보

  


-기능 테스트

브라우저마다 지원 가능한 기능을 알아본다.

  


  


 4) Window 객체

  


window.open("demo2.html"); //새 탭에 새로운 html

  


window.open("demo2.html", '\_self'); //기존 탭에서 html open *<a ~ target="\_self">

  


window.open("demo2.html", \_'blank'); //새로운 창

  


window.open("demo2.html", 'ot'); //open을 재실행 했을 때 동일한 이름의 창이 있다면 그곳으로 문서가 로드된다.

  


window.open('demo2.html', '\_black', width=200, height=200, resizable=yes'); //새 창에 대한 속성 제어

  


5) 보안

내가 클릭해서 열린 팝업창은 그대로 열리고

html 소스 상에 script 코드로 window.open으로 자동으로 열리게 되는 팝업은 제한된다.

