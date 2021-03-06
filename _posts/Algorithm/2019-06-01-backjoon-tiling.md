---
layout: post
title:  "[백준] 2xN 타일링"
date:   2019-06-01
categories: Algorithm
comments: false
---

## 문제 요약
---
링크 : [2xN 타일링](https://www.acmicpc.net/problem/11726)  

> 세로 2, 가로 N인 2xN 직사각형 타일틀이 있다.  
이 직사각형 타일 틀 안에, 세로 1, 가로 2 인 1x2 직사각형 (쉽게 생각해서 'ㅡ' 이런 형태) 과 세로 2, 가로 1 인 2x1 직사각형 ('|') 을 채워 넣을 때, 채워 넣는 방법의 개수를 구해라.

## 풀이
---
처음에는 2행 N열 짜리 배열안에 직접, '1x2 & 2x1' 을 채워 넣으면서 찾으려 했는데, 너무 복잡해 지고 시간도 많이 소요된다.  

하다보니, 규칙성을 찾게 되었다.  
2xN 직사각형을 타일틀이 있다면, 이 타일틀에 구성할 수 있는 타일 모양의 개수는, '2x(N-1)'의 방법의 수 + '2x(N-2)'의 방법의 수 라는 점화식이 도출 된다.  

해당 방법으로 나는, List 를 만들어서 N 만큼의 배열을 만들어 가면서 찾았다.
헌데, 문제에서 N 을 입력받고 '2xN' 이 경우에만 찾는 것이어서 상관은 없었지만, 여러개의 N 이 주어진다면, 배열에 이미 N 까지의 수를 다 생성해 놓고 접근하는 것이 좋을 듯 하다.  

진행을 하다보면, 경우의 수가 int 범위를 초과하는 경우가 생긴다.  
그 경우, 사칙연산에서 오류가 발생할 수 있기 때문에, 'BigInteger'로 하나씩 선언해 주면서 처리했다.

## Code
---
~~~
package backjoon;

import java.math.BigInteger;
import java.util.LinkedList;
import java.util.List;
import java.util.Scanner;
import java.util.Stack;

/*
잘 생각해 보자.

타일을 일일이 다 깔아가면서 세기가 빡세다.
규칙이 있다.

예를들어, 1차원 배열이 있다고 생각하자.
쭉 이어져 있을 것이고, 세로 타일은 '1'만큼 자리를 차지 할 테고, 가로 타일은 '2'만큼 자리를 차지 할 것이다.

구체적으로 배열의 크기를 생각해보면 배열의 크기가 1일 떄 들어갈 수 있는 타일은
[1] 뿐이 없다.

 */
public class Tiling {

  private static final Scanner scan = new Scanner(System.in);

  private void solve3(int tileLength) {
    List<BigInteger> dp = new LinkedList<>(); // 어차피 타일의 길이는 '1000'으로 한정 되어 있기 때문에, 'new int[1000]' 으로 만들어도 가능.

    dp.add(BigInteger.valueOf(1));
    dp.add(BigInteger.valueOf(2));
    dp.add(BigInteger.valueOf(3));

    if (tileLength > 3) {
      for (int i = 1; i <= tileLength - 3; i++) {

        BigInteger tmp1 = dp.get(i);
        BigInteger tmp2 = dp.get(i + 1);

        BigInteger sum = tmp1.add(tmp2);

        dp.add(sum);
      }
    }

    BigInteger factor = BigInteger.valueOf(10007);

    // 타일의 열은 '1' 부터 증가하고(2x1 -> 2x2 ... ), 해당 타일의 갯수를 저장하는 배열은 인덱스가 '0' 부터 시작.
    int N = (tileLength - 1);

    BigInteger result = dp.get(N).mod(factor);

    System.out.println(result);
  }

  // 점화식, int 범위를 넘어가는 수가 list 에 들어갈 경우 결과가 달라 질 수 있다.
  private void checker(int tileLength) {
    int[] eachTileCntArr = new int[1001];

    eachTileCntArr[1] = 1;
    eachTileCntArr[2] = 2;
    eachTileCntArr[3] = 3;

    if (tileLength > 3) {

      // 'N - 1' 까지의 타일링을 알면, 길이가 'N'인 타일링을 알 수 있다.
      int length = (tileLength - 1);

      // '2x4' 길이의 타일링 부터 구해야 한다.
      int start = 4;

      for (int i = 2; i < length; i++) {

        // int 범위를 넘어가는 숫자가 발생한다.
        if (eachTileCntArr[i] > eachTileCntArr[i + 1]) {
          System.out.format("int 범위를 넘어가는 부분 N: %d / 해당하는 부분의 값 N: %d, N + 1: %d \n",
                  start, eachTileCntArr[i], eachTileCntArr[i + 1]);
        }
        eachTileCntArr[start++] = (eachTileCntArr[i] + eachTileCntArr[i + 1]);
      }

    }
  }

  // Stack, 시간 초과
  private void solve(int tileLength) {
    int count = 0;

    int factor = 10007;

    Stack<Integer> stack = new Stack<>();

    stack.push(tileLength);

    while (stack.iterator().hasNext()) {
      int temp = stack.pop();

      for (int i = 1; i < 3; i++) {
        int result = (temp - i);

        if (result < 0) continue;

        if (result == 0) count++;
        else stack.push(result);
      }
    }

    System.out.println((count % factor));
  }

  public static void main(String[] args) {
    int N = scan.nextInt();

    if (N < 0 || N > 1000) {
      System.out.println("입력 값 오류 ( 1<= N <= 1000)");
      return;
    }

    new Tiling().checker(N);
  }
}
~~~