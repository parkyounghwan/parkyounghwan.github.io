---
layout: post
title:  "[백준] 피보나치 수"
date:   2019-06-03
categories: Algorithm
comments: false
---

## 문제 요약
---
링크 : [피보나치 수](https://www.acmicpc.net/problem/2747)  

> 피보나치 수는 첫번째 수가 '0' 이고 두번쨰 수가 '1' 로 시작을 한다.  
배열에 피보나치 수가 들어있을 때, 'n' 번째 피보나치 수를 출력해라.  
'n' 은 45 보다 작거나 같다.

## 풀이
---
미리 배열에 피보나치 수를 만들어 놓고, 입력 받은 'n' 의 배열 인덱스의 값을 출력해 주었다.  
  
만들어 둔 피보나치 배열은 인덱스가 0번째 부터 시작하는데, 입력 받는 값 'n' 은 자연수 범위 이기 때문에 사용자가 원하는 값의 시작은 __1번째__ 부터 __45번째__ 까지이다.  

따라서, 배열을 만들 때, '0'을 고려해서 배열의 크기를 '46'까지 주었다.

## Code
---
~~~
package backjoon;

import java.util.Scanner;

public class Fibonacci {

  private static final Scanner scan = new Scanner(System.in);

  private static final int N = 46;
  private static int[] fiboArr = new int[N];

  private void setArr() {
    fiboArr[0] = 0;
    fiboArr[1] = 1;

    int start = 2;  // 3번째

    for (int i = start; i < N; i++) {
      fiboArr[i] = fiboArr[i - 1] + fiboArr[i - 2];
    }
  }

  public static void main(String[] args) {
    int input = scan.nextInt();

    new Fibonacci().setArr();

    System.out.println(fiboArr[input]);
  }
}
~~~