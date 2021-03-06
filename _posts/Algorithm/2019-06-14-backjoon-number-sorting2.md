---
layout: post
title:  "[백준] 수 정렬하기2"
date:   2019-06-14
categories: Algorithm
comments: false
---

## 문제 요약
---
링크 : [수 정렬하기2](https://www.acmicpc.net/problem/2751)  

> N 개의 수가 주어졌을 때, 오름차순으로 정렬 하라.  
N 의 범위는  1 <= N <= 1,000,000, 수는 절대값이 1,000,000 이하인 정수.

## 풀이
---
제공되는 sort 메소드를 사용하면, 시간초과가 발생한다.

N 의 범위가 1,000,000 이므로 배열을 생성해서, 각 숫자에 해당하는 인덱스에 표시를 해서 배열을 순서대로 출력하는 형태로 구현.

다만, 입력받는 수의 범위가 음의 정수, 양의 정수, 0 을 고려해서 구현해야 한다.

나는 배열 인덱스를 음의 정수는 0 ~ 999,999 까지 주고 양의 정수는 1,000,001 ~ 2,000,000, 0 을 1,000,000 으로 주어서 표현했다.

## Code
---
~~~
package backjoon;

import java.util.Scanner;

public class NumberSort2 {

  private static final Scanner scan = new Scanner(System.in);

  public static void main(String[] args) {
    int N = scan.nextInt();
    scan.nextLine();

    int intScope = 1000000;
    int scope = (intScope + intScope + 1);  // 음의 정수 + 양의 정수 + '0'

    int[] arr = new int[scope];

    for (int i = 0; i < N; i++) {
      int num = scan.nextInt();

      arr[(intScope + num)] = 1;
    }

    for (int i = 0; i < scope; i++) {
      if (arr[i] != 0) {
        System.out.println(i - intScope);
      }
    }
  }
}
~~~