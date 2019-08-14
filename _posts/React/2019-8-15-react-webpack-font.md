---
layout: post
title:  "React 폰트 적용 (with, webpack)"
date:   2019-08-15
categories: React
comments: false
---

사용지점

* React, webpack 을 통한 프론트엔드 개발 중
* 웹 폰트를 다운 받아놓은 상태, 확장자는 '.TTF' / '.orf'

<br/>

진행방향

* 웹 폰트를 다운 받아서 적용하는 시나리오.
* 폰트 또한 파일 이기 때문에, '…-loader' 가 필요하고 추가적으로 webpack 설정이 더 들어간다.

<br/>

### 폰트 파일 유형

* EOT (Embedded Open Type) : IE 에서만 통용.
* TrueType / OpenType : '.ttf(TrueType format)' 과 '.otf(OpenType format)' 의 확장자를 갖으며, 컴퓨터 서체 파일로 널리 사용되는 파일 형식
  * 웹 뿐만 아니라 전자 출판에도 사용 가능.
  * 대부분의 브라우저에서 지원
* WOFF (Web Open Font Format) : 웹을 주된 대상으로 설계된 파일 형식
  * 'TrueType' 이나 'OpenType' 서체를 압축한 것이기 때문에 일반적으로 파일 크기가 작아서, 다른 서체보다 신속히 다운됨.
  * 안드로이드 진영에서는 사용 불가.
* SVG (Scalable Vector Graphic) : 본질이 서체 파일은 아님, 벡터 그래픽 (확대해도 품질이 유지되는 이미지를 만드는 기술) 
  * SVG 폰트를 지원하는 브라우저는 매우 제한적.
  * 파일 크기가 'TrueType' 의 2배, 'WOFF' 파일의 3배에 달한다.
  * iOS, 사파리4.1 이전 버전에서 인식하는 유일한 웹 폰트 타입.

<br/>

### 웹 폰트 사용

두 개의 CSS 명령어 필요

* **@font-face** : 웹 브라우저에게 서체 이름과 다운 받을 위치(저장 되어 있는 위치)
* **font-family** : 이름 지정 및 사용

<br/>

### 파일 변환

가능한 많은 브라우저가 사용할 수 있도록 폰트를 제공하려면, **EOT, WOFF, TureType** 서체는 제공해야 한다.

> [Font Squirrel](https://www.fontsquirrel.com/tools/webfont-generator), 폰트 변환 사이트

사용하고자 하는  '.ttf' 서체나 '.otf' 서체를 업로드 하여 변환해 준다.

<br/>

### 코드

* '.css'

  * 페이지 전체에 적용 될 수 있는, root 급(html, body 태그 스타일을 먹일 수 있는) css 파일에 명시
  * 명시 후에, 원하는 부분에 _font-family_ 로 이름 적용해서 사용

  <img width="716" alt="스크린샷 2019-08-15 오전 3 43 34" src="https://user-images.githubusercontent.com/20623970/63047225-f73e1880-bf0e-11e9-8e12-416f6822c49e.png">

  <br/>

* webpack

  * npm 'url-loader' 설치 후, 설정 추가

  <img width="752" alt="스크린샷 2019-08-15 오전 3 45 32" src="https://user-images.githubusercontent.com/20623970/63047371-484e0c80-bf0f-11e9-8e77-8ba54cc02c48.png">

  