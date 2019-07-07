---
layout: post
title:  "[백준] 최소 공배수"
date:   2019-07-07
categories: Algorithm
comments: false
---

## 문제 요약
---
링크 : [최소 공배수](https://www.acmicpc.net/problem/1934)  

> 두 수 a, b 가 주어졌을 때, 최소 공배수를 구하는 문제.

<br/>
<br/>

## 풀이
---
최대 공약수를 구한 다음에, 각 수 a, b 를 최대공약수로 나눈 몫을 곱하는 식으로 최소 공배수를 구함.  

최대 공약수를 구하는 방법 중에, 유클리드 호제법을 사용하는 방식이 있다.  

<br/>

**유클리드 호제법**
두 수 a, b 가 있을 때 'a 가 b 보다 크다' 고 가정 하자.  
a 와 b 의 최대 공약수는 a 를 b 로 나눈 나머지 r 과 b 의 최대 공약수와 같다.  

'a, b 의 최대 공약수' == '(a % b), b 의 최대 공약수'  

이 과정을 반복해서, 나머지 r 이 '0' 이 나올 때 까지 구하면, 그 수가 a, b 의 최대 공약수가 된다.

<br/>

위 호제법을 구하는 역러가지 방식 중에 재귀를 이용한 방식이 참신하여 정리한다.  

보통 'a > b' 의 크기를 비교해서 나머지를 찾기 마련인데, 아래 코드는 그 과정을 수학적인 연산으로 생략했다.  

'a / b' 라고 할 때, a 는 피제수 이고, b 는 제수라고 부른다.  
예를들어, '6 % 15' 라고 하면, 어떻게 될까? 나뉨 수 6 (피제수) 가 나눔 수 15 (제수) 보다 작을 경우 자기 자신이 나오는 성질을 이용해서 'a > b' 를 비교하는 과정을 생략할 수 있다.

~~~
public int GCD (int a, int b) {
    if (b == 0) {
        return a;
    } else {
        return GCD (b, (a % b));
    }
}
~~~
<br/>
<br/>

## Code
---
~~~
package backjoon;

import java.util.Scanner;

public class LeastCommonMultiple {

  private int GCD(int a, int b) {
    if (b == 0) {
      return a;
    } else {
      return GCD(b, (a % b));
    }
  }

  private int LCM(int a, int b, int GCD) {
    return (a*b/GCD);
  }

  public static void main(String[] args) {
    Scanner scan = new Scanner(System.in);

    int N = scan.nextInt();
    scan.nextLine();

    StringBuilder sb = new StringBuilder();

    for (int i = 0; i < N; i++) {
      String[] inputs = scan.nextLine().split(" ");
      int a = Integer.parseInt(inputs[0]);
      int b = Integer.parseInt(inputs[1]);

      int gcd = new LeastCommonMultiple().GCD(a, b);
      int result = new LeastCommonMultiple().LCM(a, b, gcd);

      if (i == (N - 1)) sb.append(result);
      else sb.append(result + "\n");
    }

    System.out.println(sb.toString());
  }
}
~~~