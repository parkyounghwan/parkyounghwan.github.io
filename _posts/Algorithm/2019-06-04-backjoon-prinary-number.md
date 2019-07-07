---
layout: post
title:  "[백준] 이친수"
date:   2019-06-04
categories: Algorithm
comments: false
---

## 문제 요약
---
링크 : [이친수](https://www.acmicpc.net/problem/2193)  

> 자리수 N 이 주어졌을 때, 다음의 규칙을 만족하는 수의 개수를 찾아라.
>> 0. 이친수는 '0'과 '1'로 이루어진 수
>> 1. '1'로 시작한다.
>> 2. '1' 다음에 연속으로 '1'이 올 수 없다.  
    (ex, 11 - X / 10, 101, 1, 100010 - O)

## 풀이
---
1번째 : [1]  
2번째 : [10]  
3번째 : [100, 101]  
4번째 : [1000, 1001] / [1010]  
5번째 : [10000, 10001] / [10010] / [10100, 10101]  
6번째 : [100000, 100001] / [100010] / [100100, 100101] / [101000, 101001] / [101010]  

자세히 보면, 끝자리가 '0'으로 끝나는 경우 뒤에 붙일 수 있는 수가 '0', '1' 두가지 이고,  
'1'로 끝나는 경우 '0' 뿐이 붙이지 못한다.  

이를 착안하여, 끝자리가 '0'인 개수와 '1'인 개수를 확인해서 다음의 결과를 예측한다.  

1. N행 2열 짜리 배열을 만든다. (0열은 '0'의 개수 / 1열은 '1'의 개수)
2. 첫행은 arr[0][0] = 0 / arr[0][1] = 1 로 초기화 (끝자리 기준으로, 0인 것은 없고, 1인 것은 1개)
3. 다음 행의 개수를 전 행의 결과로 추가해 준다.  
    전 행의 '0'의 개수가 존재 한다면 arr[k][0] 도 증가하고, arr[k][1] 도 증가한다.  
    '1'의 개수가 존재한다면 arr[k][0] 의 개수만 증가한다.
4. 증가하는 비율은 전 행의 개수 만큼 씩 증가한다.  
5. 개수의 범위가 int 를 벗어나 long 으로 맞춰줌.


## Code
---
~~~
package backjoon;

import java.math.BigInteger;
import java.util.Arrays;
import java.util.LinkedList;
import java.util.Queue;
import java.util.Scanner;

public class PrinaryNumber {

  private static final Scanner scan = new Scanner(System.in);

  /*
  1이면 경우의 수가 '0' 이 오는 것 하나
  0이면 경우의 수가 '0'이 오는 것과 '1'이 오는 것 두개
   */
  private void solve(int N) {
    long[][] dp = new long[N][2];  // 0열 은 '0'의 갯수, 1열은 '1'의 갯수
    dp[0][0] = 0;
    dp[0][1] = 1;

    for (int i = 1; i < N; i++) {
      //전 과정에서 '1'의 갯수가 1개 존재하면, 다음에도 한개인데 '0'의 갯수에 추가해주어야한다.
      if(dp[i - 1][1] > 0) {
        dp[i][0] += (dp[i - 1][1]);
      }

      // 전 과정에서 '0'이 존재하면,
      if(dp[i - 1][0] > 0) {
        dp[i][0] += dp[i - 1][0];
        dp[i][1] += dp[i - 1][0];
      }
    }

    System.out.format("0의 갯수: %d, 1의 갯수: %d \n", dp[N - 1][0], dp[N - 1][1]);
  }

  public static void main(String[] args) {
    int N = scan.nextInt();

    new PrinaryNumber().solve(N);
  }
}

~~~