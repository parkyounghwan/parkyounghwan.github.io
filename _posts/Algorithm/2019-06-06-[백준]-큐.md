---
layout: post
title:  "[백준] 큐"
date:   2019-06-06
categories: Algorithm
comments: false
---

## 문제 요약
---
링크 : [큐](https://www.acmicpc.net/problem/10845)  

> 첫 줄에 명령어의 개수 T 가 주어지고, T 만큼 명령어가 주어질 때, 다음에 만족하는 결과값을 출력하라.
>>push X: 정수 X를 큐에 넣는 연산이다.  
pop: 큐에서 가장 앞에 있는 정수를 빼고, 그 수를 출력한다. 만약 큐에 들어있는 정수가 없는 경우에는 -1을 출력한다.  
size: 큐에 들어있는 정수의 개수를 출력한다.  
empty: 큐가 비어있으면 1, 아니면 0을 출력한다.  
front: 큐의 가장 앞에 있는 정수를 출력한다. 만약 큐에 들어있는 정수가 없는 경우에는 -1을 출력한다.  
back: 큐의 가장 뒤에 있는 정수를 출력한다. 만약 큐에 들어있는 정수가 없는 경우에는 -1을 출력한다.  

## 풀이
---
큐 구현
1차원 배열을 사용해서 큐를 구현한다.

1. 포인트를 체크해 주어야 한다.   
: 'Front' 와 'End'
2. 배열 사이즈를 산정해야 한다.  
: 문제에서 사이즈를 정해주어서 동적으로 구현할 필요는 없지만, 해보면 좋을 듯 하다.

## Code
---
~~~
package backjoon;

import java.util.Scanner;

public class Queue {

  private static final Scanner scan = new Scanner(System.in);

  public static class Que {
    private int[] ARR;
    private int FRONT;
    private int INDEX;

    public Que() {
      this.ARR = new int[10000];
      this.FRONT = -1;
      this.INDEX = -1;
    }

    public void solve(String[] comm) {

      for (int i = 0; i < comm.length; i++) {

        if (comm[i].contains("push")) {
          String[] values = comm[i].split(" ");
          push(Integer.parseInt(values[1]));
        } else {
          switch (comm[i]) {
            case "pop":
              System.out.println(pop());
              break;
            case "empty":
              System.out.println(isEmpty());
              break;
            case "front":
              System.out.println(getFront());
              break;
            case "back":
              System.out.println(getREAR());
              break;
            case "size":
              System.out.println(getSize());
              break;
          }
        }

      }
    }

    private void push(int num) {
      ARR[++INDEX] = num;
    }

    // size: 큐에 들어있는 정수의 개수를 출력한다.
    private int getSize() {
      return (INDEX - FRONT);
    }

    //front: 큐의 가장 앞에 있는 정수를 출력한다. 만약 큐에 들어있는 정수가 없는 경우에는 -1을 출력한다.
    private int getFront() {
      return (getSize() == 0) ? -1 : ARR[FRONT + 1];
    }

    private int getREAR() {
      return (getSize() == 0) ? -1 : ARR[INDEX];
    }

    //empty: 큐가 비어있으면 1, 아니면 0을 출력한다.
    private int isEmpty() {
      return (INDEX == FRONT) ? 1 : 0;
    }

    // 큐에서 가장 앞에 있는 정수를 빼고, 그 수를 출력한다. 만약 큐에 들어있는 정수가 없는 경우에는 -1을 출력한다.
    private int pop() {
      if(INDEX > FRONT) return ARR[++FRONT];
      else return -1;
    }
  }

  public static void main(String[] args) {
    int T = scan.nextInt();
    scan.nextLine();

    String[] comm = new String[T];

    for (int i = 0; i < T; i++) {
      String input = scan.nextLine();

      comm[i] = input;
    }

    Que que = new Que();
    que.solve(comm);
  }
}
~~~