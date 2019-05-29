---
layout: post
title:  "[Android-Studio]-기본적인-버튼-클릭-이벤트-처리."
date:   2016-09-07 
categories: Android-Studio
comments: false
---
-정리하는 이유는 책이나 여타 블로그에서 보던 메소드에서 안되던 부분이어서 정리한다.  


  


-그냥 진짜 기본적으로 Button 객체 생성하고 이벤트 처리하게 만들 것.  


  


-Button의 특징 몇개만 잡고 간다.

*Button은 TextView의 하위 클래스이며 TextView의 여러 기능을 사용할 수 있다.

*TextView에서도 Button 클릭 같은 이벤트를 발생 시킬 수 있다.

  


-레이아웃(Activity Layout 리소스 XML에 Button 추가)

  


-Java source

***Activity의 Layout 리소스 XML에 Button을 추가할 때 지정한 "id" 속성 값을 사용하여 Button에 대한 참조를 획득 할 수 있다.**

  


-Button 클릭에 대한 이벤트 처리.

*안드로이드에서는 위젯에서 발생한 특정 이벤트를 처리하기 위해 리스터(Listener)라는 것을 사용한다.

*Listener : 어떤 이벤트의 발생 여부에 귀기울이는 객체.

*Button에서 발생할 수 있는 클릭 이벤트는 부모 클래스인 View클래스에 이미 정의되어 있다.

*클릭 이벤트를 위한 Listener도 java 인터페이스의 형태로 정의되어 있다.

*이벤트 발생 시 호출될 함수의 형식(이름, 파라미터, 리턴 값)도 인터페이스 내에 정의되어 있다.

*Listener 객체가 Button의 클릭 이벤트를 처리할 것인지 지정하는 함수까지 만들어져 있다.

*이벤트 발생 시 호출될 함수를 구현한 리스너 객체를 생성하여 Button에 지정 하기만 하면 된다.

  


  


-책에 나온 코드는 Button에 지정해 주는 부분이 빠져있어서 오류가 났다.

  


