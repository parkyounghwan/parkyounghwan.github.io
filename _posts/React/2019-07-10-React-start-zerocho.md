---
layout: post
title:  "React 란 무엇인가? 왜 쓰는가? - zerocho"
date:   2019-07-10 
categories: React
comments: false
---

사용자 인터페이스를 만들기 위한 JS 라이브러리 / 프레임워크

 <br/>

## 싱글페이지 어플리케이션

---

웹에서 앱의 사용자 경험을 주기 위해서

<br/>

## 페이스북

---

데이터랑 화면이랑 일치시키는 문제가 어렵기 때문에, React 가 알아서 해준다.

<br/>

## 컴포넌트

---

웹에서 중복되는 부분을 조각으로 만들어서 중복을 피할 수 있게 한다.

유지보수 하기가 좋다.

<br/>

## This

---

* 화살표 함수와, function 쓰는 함수의 차이

~~~javascript
class Foo extends React.Component {
	constructor(props) {
    super(props);
    
    // 상태, 웹 페이지 상에서 컴포넌트의 내용이 변하는 것들.
    this.state = {
      first: '',
      second: Math.ceil(Math.random() * 9),
      ...
    }
    
    this.onSubmit = this.onSubmit.bind(this);
  }
  
  // function
  onSubmit = function (e) { 
  	this.setState({value: e.target.value});
  }
  
  // arrow function
  onCraete = () => { ... }
  
  render() {
    return (
        <React.Fragment>
      		<input ref={this.onSubmit}/>
        </React.Fragment>
      )
  }
}
~~~

* _Class_ 내부에 화살표 함수로 메소드를 만들면 _render()_ 에서 쓸 때, this.[method-name] 으로 호출이 가능하다.
* 이 때 _this_ 로 _Foo_ 클래스의 메소드 호출을 명시 할 수 있는데, _function_ 으로 메소드를 만들면, _onSubmit_ 메소드 내부의 this 가 _function_ 을 가리키게 되어서, 상태값, _state_ 를 변경하려는 우리의 목적과 달라진다.
* 따라서, 만약 _function_ 을 써야 한다면, _constructor_ 에 'this.onSubmit = this.onSubmit.bind(this);' 로 this 의 주인을 설정해 주어야 한다.

<br/>

## document.querySelector('input').focus()

---

비구조화 할당, 구조 분해 할당, Distructure

jQuery 는 선택자를 사용해서 DOM 에 접근할 수 있지만, 페이지 전체를 스켄 해야 한다.  

다시말해, 특정 태그 및 선택자를 찾기 위해 모든 DOM 노드를 순회해야 한다.

<br/>

## Class vs Hooks

---

* Class

  ~~~javascript
  class Foo extends React.Component {
    ...
    
    render() {
      return ... ;
    }
  }
  ~~~

  * 웹 페이지 상에서, _state_ 값이 변할 때 마다, _Foo_ 클래스의 _render_ 함수가 호출 되는 구조.

<br/>

* Hooks

  ~~~javascript
  const Foo = () => {
    ...
    
    return ... ;
  }
  ~~~

  * _Foo_ 함수 전체가 계속 호출 되는 구조

결론적으로 _Class_ 형식 보다 _Hooks_ 구조로 짜는 것이 조금 더 느리다.

<br/>

## WebPack

---

여러가지 컴포넌트를 하나로 관리하기 위한 도구.  

webpack 을 돌리기 위한 js 실행기 인 node 가 깔려 있어야 한다.  

페이스북의 컴포넌트는 2만개 정도 있다고 한다. 하나의 파일에 2만개의 컴포넌트를 관리한다면, 유지보수는 불가능한 수준일 것이다.   

컴포넌트 파일을 분리해서 사용하기 위한 기술이 _WebPack_ 이며, 각 컴포넌트 파일에서 어떤 파일을 import 받는지도 관리해준다.  

마치 스프링에서 빈을 관리하는 느낌.

<br/>

## JSX vs JS

---

JSX 문법을 적으면 JSX 파일로 만드는 것이 좋다.

'아 이 파일은 JSX 문법을 담고 있구나, React 구나'

<br/>
<br/>

### tip

* 태그 작성 시, 속성 명칭 이슈
  * class -> className
  * for -> htmlFor

