---
layout: post
title:  "[백준] 1, 2, 3 더하기"
date:   2019-05-30
categories: Algorithm
comments: false
---

## 문제 요약
---
링크 : [1, 2, 3 더하기](https://www.acmicpc.net/status?user_id=dudrnxps&problem_id=9095&from_mine=1)

> 11 보다 작은 양수 N 이 주어 질 때, '1', '2', '3' 을 이용해서, N 을 만들 수 있는 경우의 수를 모두 구하라.  
위 제시 된 3 수 (1,2,3)은 중복이 가능하며, '1+2' 와 '2+1' 은 다른 경우의 수로 취급한다.

## 풀이
---
모든 경우의 수를 다 생각해 보아야 한다.  

예를들어, [1] / [2] / [3] / [1, 2] / [1, 3] / [2, 3] / [1, 2, 3] 으로 N 을 만들 수 있는 경우를 찾아야 한다.

N 을 만들기 위해 각 수, '1', '2', '3' 을 N 에서 뺸 결과 값을 가지고 '0'이 될 때 까지 돌려 준다.  

N 이 '0'이 되는 순간 경우의 수를 찾는 것으로 판단.  

## Code
---
~~~
package backjoon;

import java.util.*;

public class OneTwoThreePlus {

  private static final Scanner scan = new Scanner(System.in);

  /*
  주어진 N 에 대해서 '1', '2', '3'을 뺀 결과를 바탕으로 반복하여 결과가 '0' 이 되는 경우를 카운트 한다.
   */
  private int solve(int N) {
    int count = 0;

    Queue<Integer> leftValues = new LinkedList<>();
    leftValues.add(N);

    while (leftValues.iterator().hasNext()) {
      int num = leftValues.poll();

      for (int i = 1; i < 4; i++) {     // '1', '2', '3'

        int result = (num - i);

        if (result < 0) continue;       // 뺀 결과가 '0' 보다 작을 경우 그냥 넘긴다
        else {

          if (result == 0) count++;
          else leftValues.add(result);      // 다음 경우의 수가 있는지 판단하기 위해 Queue 에 삽입

        }

      }

    }

    return count;
  }

  public static void main(String[] args) {
    int T = scan.nextInt();

    int[] arr = new int[T];
    for (int i = 0; i < T; i++) {
      int N = scan.nextInt();

      if (N < 0 || N > 11) continue;
      else arr[i] = N;
    }

    for (int i = 0; i < T; i++) {
      System.out.println(new OneTwoThreePlus().solve(arr[i]));
    }
  }
}
~~~