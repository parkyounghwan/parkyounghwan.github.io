---
layout: post
title:  "[백준] 1로 만들기"
date:   2019-05-29
categories: Algorithm
comments: false
---

## 문제 요약
---
링크 : [1로 만들기](https://www.acmicpc.net/problem/1463)

> 입력 받은 정수 N 이 있다.   
이 N 을   
i. 3 으로 나누어서 나누어 떨어지면 3으로 나누고  
ii. 2 로 나누어서 나누어 떨어지면 2로 나누고
iii. 아니면 1 을 뺴서  
'1' 로 만들어야 한다.  
이떄, 가장 적은 산술을 통해서 '1'을 만드는 경우를 출력해야 한다.

## 풀이
---
일단, 3가지 경우의 수를 모두 경험 시켜야 한다.  

'3으로 나누어 떨어질 때', '2로 나누어 떨어질 때', '1을 뺄 때' 이 세가지 수의 결과로 다시 3가지 경우의 수를 돌려야 한다.  
  
나는 Queue 를 사용해서, 위 경우의 수를 돌려서 나온 결과를 다시 Queue 만큼 돌려서 확인했다.
  
Queue 를 돌릴 때, '0'이 나오거나, 3 이나 2 로 나누어 떨어지지 않는 수는 Queue 에 넣지 않으면서 확인했다.  

## Code
---
~~~
package backjoon;

import java.util.*;

public class MakeOne {

  private static final Scanner scan = new Scanner(System.in);

  private void solve(int N) {
    int result = 0;

    Queue<Integer> dpList = new LinkedList<>();
    dpList.add(N);

    while (!dpList.isEmpty()) {
      int qSize = dpList.size();

      boolean flag = false;
      for (int i = 0; i < qSize; i++) {
        int num = dpList.poll();

        int temp1 = 0;
        int temp2 = 0;
        int temp3;

        if ((num % 3) == 0) {
          temp1 = (num / 3);
          if (temp1 != 0) dpList.add(temp1);
        }

        if ((num % 2) == 0) {
          temp2 = (num / 2);
          if (temp2 != 0) dpList.add(temp2);
        }

        temp3 = (num - 1);
        if (temp3 != 0) dpList.add(temp3);

        if ((temp1 == 1) || (temp2 == 1) || (temp3 == 1)) {
          flag = true;
          break;
        }

      }
      if(!dpList.isEmpty()) result++; // 카운트 조건

      if(flag) break;
    }

    System.out.println(result);
  }

  public static void main(String[] args) {
    int N = scan.nextInt();

    new MakeOne().solve(N);
  }
}
~~~