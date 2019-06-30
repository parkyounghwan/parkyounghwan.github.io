---
layout: post
date:   2019-06-29 
categories: JavaScript
slug: styleguide
comments: false
---

유수의 회사에서는 어떻게 컨벤션을 적용하는지 알아보고, 과연 프로젝트를 진행 할 떄, 컨벤션이 어떤 영향을 미치게 되는지 알아본다.

컨벤션은 여러 단어로 불려 지기도 한다. 우리 나라에서는 컨벤션으로 자주 불리는 것 같고, 외국에서는 스타일 가이드 정도로 부르고 있는 것 같다.

<br />

## 왜 컨벤션을 적용하려고 하는가?

---

자바스크립트 자체가 다양한 스타일 선택을 허용하고 관대하기 때문에 협업 시, 정리가 한번 필요하다고 생각했다.

ES5 와 ES6 에서 쓰이는 문법에 대한 사전 지식이 없는 상태에서, 구글링 시에 참고 할 코드들을 선별하고 적용해야 할 필요성을 느꼈다. 로직은 가져오되 문법만 바꿔주면 되는 문제이긴 하지만 적립 시키기를 원했다.  

또한, 새미콜론 / 괄호 / Tab / 띄어쓰기 등의 스타일 이슈를 통일 시켜서 협업 시 코드 가독성을 높이고자 했다.  

<br/>

## 얻을 수 있는 효과

---

처음에는 컨벤션 자체를 하나 하나 정의 한 후, 코드를 작성하면서 맞추려고 했다. Lint 의 존재를 알고 있긴 했지만, 런타임 시 deprecated 나 문법 만 맞춰주는 것으로 생각했는데, 스타일 부분까지 맞춰 주는 사실을 알고 Lint 를 사용하기로 했다.

Lint 를 적용하면서 코드를 작성하며 맞출 수 있었고, 원본 파일 전체에 걸쳐 일관된 스타일을 적용 시킬 수 있다.

<br />

## 스타일 가이드 종류

---

Lint 를 적용하면서, 유수의 회사들에서 쓰는 규칙들이 있다는 것을 알았고, Google / Airbnb 의 스타일 가이드가 가장 많이 검색 되었다. Naver 의 경우 Airbnb 의 규칙을 빌려서 커스텀 한 것으로 보인다.

스타일 가이드는 5가지 정도를 찾아볼 수 있었다.

* [Airbnb](https://github.com/airbnb/javascript)
* [Google](https://google.github.io/styleguide/jsguide.html)
* [관용적인 JavaScript](https://github.com/rwaldron/idiomatic.js/)
* [JavaScript 표준](https://github.com/standard/standard)
* [jQuery JavaScript](https://contribute.jquery.org/style-guide/js/)  

<br/>

## 어떤 것을 적용할 것인가

---

우리는 유명한 회사에서 쓰이는 스타일 가이드를 참고하기로 했고, Google / Airbnb 둘 중에 하나를 선택하고자 한다. Airbnb 의 경우 Google 보다 더 넓은 범위에서 상세하게 가이드 하고 있었고, 아래 와 같은 차이가 있다.  

<br/>

### Google vs Airbnb

---

Airbnb 기준으로 비교를 한 자료이고, [블로그](https://ohgyun.com/m/609?category=197866)를 참고하여 작성했다.

* 함수

  함수 정의 시 **표현식** 대신 **선언식** 사용. 호이스팅 이슈를 해결하고, _Arrow Function_ 으로 축약 표현이 장점. (현재는 둘 다 Arrow Function 사용)  

  ~~~javascript
  // Bad
  [1, 2, 3].map(function (x) {
    const y = x + 1;
    return x * y;
  });
  
  // Good
  [1,2,3].map((x) => {
    const y = x + 1;
    return x * y;
  })
  ~~~

<br/>

* 긴 문자열의 사용

  Google 의 경우 문자열이 길어 질 경우 '**+**' 연산자를 사용해서, 표현  

  ~~~javascript
  // Google
  const errorMessage = 'This is a super long error that was thrown because ' +
        'of Batman. When you stop to think about how Batman had anything to do' +
        'with this, you would get nowhere fast.';
  
  // Airbnb
  const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think  about how Batman had anything to do with this, you would get nowhere fast.';
  ~~~

  > Airbnb 스타일 가이드에 따르면, 나뉜 문자열의 경우 코드 검색을 어렵게 한다는 이유를 명시해 놓았다.

<br/>

* 작은 따옴표와 _Template String_

  Google 과 Airbnb 스타일 가이드 둘 다, 비슷한데 Airbnb 쪽이 조금 더 디테일하다.

  Template String 의 경우 Google 은 프로그래밍 방식의 문자열의 경우에만 예시를 보여주고 있다.

  Airbnb 의 경우 문자열 내에 작은 따옴표가 있는 경우나 이스케이프( \ )가 필요한 경우에도 예시를 보여준다.  

  

  * Template String 

    ~~~javascript
    // Google
    function arthmetic(a, b) {
      return `Here is a table of arithmetic operations: 
    $(a) + $(b) = $(a + b)
    $(a) - $(b) = $(a  b)
    $(a) * $(b) = $(a * b)
    $(a) / $(b) = $(a / b)`;
    }
    
    // Airbnb
    // Bad - 템플릿 문자열의 간격의 사용을 없애는 것으로 강제한다. (ESLint 에서 default로 적용)
    function sayHi(name) {
      return `How are you, ${ name }?`;
    }
    
    // Good
    function sayHi(name) {
      return `How are you, ${name}?`;
    }
    ~~~
  
  <br/>
  
  * Escape, 불필요한 이스케이프의 사용을 허용하지 않는다. (ESLint) - 이 가이드는 **Airbnb** 에만 명시되어 있다.

    ~~~javascript
    //Airbnb
    // bad
    const foo = '\'this\' \i\s \"quoted\"';
    
    // good
    const foo = '\'this\' is "quoted"';
    const foo = `my name is '${name}'`;
    ~~~

<br/>

* 객체 정의 시 마지막 컴마를 표시  

  컴마를 생략 할 경우, 속성을 추가할 때 Git diff 가 이쁘게 나오지 않는다고 한다.  

<br/>

* 클래스는 _Pascal Case_ 로 작성  

  Google 과 동일 한데, 첫 글자가 대문자인 CamelCase 를 PascalCase 라고 한다.  

<br/>

* _context_ 를 저장하는 용도의 변수(self)를 사용하지 않음  

  대신 _bind_ 나 _Arrow Function_ 을 사용.

<br/>

Airbnb 의 경우 ES6+ 를 활용하였다는 이야기가 있고, 정리해보면서 ESLint 에서 제공하는 스타일을 많이 인용해 놓았고, Google 의 가이드 보다 좀 더 디테일하게 정의해 놓은 것으로 보인다.

<br />

## 실무에서 컨벤션에 대한 요구사항

---

회사마다 스타일 가이드에 대한 정의를 두 양대 산맥의 가이드를 빌려, 커스텀하게 쓰고 있는 것 같다. 이미 잘 정리되어 있는 가이드 중에서 마음에 드는 것을 골라 사용하면 될 문제이며, 하나 하나 정리해서 스타일을 정리 할 수도 있지만 시간 낭비이고, 트렌드에 맞게 또는 회사에 맞게 Lint 를 사용해 적용해서 사용하면 된다.

<br/>

## 우리 프로젝트에서는?

---

우리 프로젝트는 팀원들이 자바 스크립트에 대한 지식이 부족하고, 배워가는 과정이기 때문에 왜 이렇게 정리되었고, 왜 이렇게 사용하는지에 대한 요구사항이 있을 수 있다. 따라서 조금 더 디테일 하게 구성되어 있는 **Airbnb 스타일 가이드**를 따르기로 결정했다.

<br/>

---

* 참고 사이트  
  -[디자인 번역 공장]([https://www.vobour.com/%EA%B5%AC%EA%B8%80%EC%9D%80-%EC%9E%90%EB%B0%94-%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%8A%A4%ED%83%80%EC%9D%BC-%EA%B0%80%EC%9D%B4%EB%93%9C%EB%A5%BC-%EB%B0%9C%ED%96%89-%ED%95%A9%EB%8B%88%EB%8B%A4-%EB%8B%A4%EC%9D%8C%EC%9D%80-%EB%AA%87-%EA%B0%80%EC%A7%80-%ED%95%B5%EC%8B%AC](https://www.vobour.com/구글은-자바-스크립트-스타일-가이드를-발행-합니다-다음은-몇-가지-핵심))  
  -[Google JavaScript Style Guide](https://google.github.io/styleguide/jsguide.html#disallowed-features)  
-[Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)
