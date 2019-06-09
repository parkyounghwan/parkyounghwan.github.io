---
layout: post
title:  "[백준] 숨바꼭질"
date:   2019-06-09
categories: Algorithm
comments: false
---

## 문제 요약
---
링크 : [숨바꼭질](https://www.acmicpc.net/problem/1697)  

> 1차원 배열 안에 N, K 가 주어진다. N 이 특정 규칙을 만족하며, K 에 닿는 최소 횟수를 구하라.
>> N 은 '+1', '-1', '2N' 으로 배열 안에서 움직인다.  
N 과 K 의 범위는 0 보다 크거나 같고, 100,000 보다 작거나 같다.


## 풀이
---
N 이 움직이는 경우의 수를 모두 따져보면서, K 에 닿는 최소 횟수를 구해야 한다.  
  
1. N 의 범위는 '0 <= N >= 100,000' 이므로 배열의 갯수는 '100,001' 이 된다.
2. N 과 K 가 처음부터 같은 위치에 있을 때를 고려해야 한다.
3. BFS 로 구현 했으며, 한 회가 진행 될 때 횟수를 count 해주어야 한다.

## Code
---
~~~
package backjoon;

import java.util.LinkedList;
import java.util.Queue;
import java.util.Scanner;

public class HideAndSeek {

  private static final Scanner scan = new Scanner(System.in);

  private static boolean[] map = new boolean[100001];

  public int solve(int N, int K) {
    int result = 0;

    Queue<Integer> queue = new LinkedList<>();

    queue.add(N);
    map[N] = true;
    boolean flag = false;

    while(!flag) {
      int size = queue.size();

      boolean cntFlag = false;

      for (int i = 0; i < size; i++) {
        int next = queue.poll();

        // N 과 K 가 처음부터 같을 경우 및 이동 후 발견 한 경우.
        if(next == K) {
          flag = true;
          break;
        }

        if (next < 0 || next > 100000) continue;

        int A = next + 1;
        int B = next - 1;
        int C = next * 2;

        if (A >= 0 && A <= 100000) {
          if (!map[A]) {
            queue.add(A);
            map[A] = true;
            cntFlag = true;
          }
        }

        if (B >= 0 && B <= 100000) {
          if (!map[B]) {
            queue.add(B);
            map[B] = true;
            cntFlag = true;
          }
        }

        if (C >= 0 && C <= 100000) {
          if (!map[C]) {
            queue.add(C);
            map[C] = true;
            cntFlag = true;
          }
        }

        if (A == K || B == K || C == K) {
          flag = true;
          break;
        }
      }

      if(cntFlag) result++;

      if (flag) break;
    }

    return result;
  }

  public static void main(String[] args) {
    int N = scan.nextInt();
    int K = scan.nextInt();

    if(N < 0 || N > 100000 || K < 0 || K > 100000) return;

    int result = new HideAndSeek().solve(N, K);

    System.out.println(result);
  }
}
~~~