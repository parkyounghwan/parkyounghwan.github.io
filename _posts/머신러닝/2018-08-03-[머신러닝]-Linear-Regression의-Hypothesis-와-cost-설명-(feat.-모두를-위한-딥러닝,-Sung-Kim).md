---
layout: post
title:  "[머신러닝]-Linear-Regression의-Hypothesis-와-cost-설명-(feat.-모두를-위한-딥러닝,-Sung-Kim)"
date:   2018-08-03 
categories: 머신러닝
comments: false
---
* Hypothesis (가설), 하이파싀시스

- Linear

![](https://t1.daumcdn.net/cfile/tistory/9909A1425B64676727)

  


  


: H(x) = Wx + b

: 어떤 직선이 좋은 가설을 나타내는 것일까?

=> 실제 데이터와 가설과의 거리(차이)가 적은 것이 좋은 가설.

  


![](https://t1.daumcdn.net/cfile/tistory/9923B0435B646A1B0F)

  


* Cost function

- 가설과의 차이, H(x) - a 의 제곱.

- 주어진 데이터들과 가설과의 차이에 평균

![](https://t1.daumcdn.net/cfile/tistory/998022475B646ADE09) => H(x), 가설(예측된 가설) / y, 실제 데이터

  


  


- 가장 작은 W, b를 구하는 것이 Linear regression(리니어 리그레이션, 본토발음)의 학습이 되겠다.

  


![](https://t1.daumcdn.net/cfile/tistory/999BE6435B646C8E1E)

=> '어떤 가설이 가장 좋은 가설일까?' 에 대한 물음의 종착지이다. 

=> W, b 의 값이 가장 작은 것, 차이가 가장 적은 것이 가장 좋은 가설이고 예측값이 되겠다.

  


* Goal: Minimize cost

=> ***minimize cost(W, b)***

  


