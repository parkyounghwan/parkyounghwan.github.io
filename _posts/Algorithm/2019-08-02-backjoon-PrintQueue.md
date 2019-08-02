---
layout: post
title:  "[백준] 프린터 큐"
date:   2019-08-02
categories: Algorithm
comments: false
---

## 문제 요약
---
링크 : [프린터 큐](https://www.acmicpc.net/problem/1966)  

> _링크 참조_
* 큐에 제일 앞에 있는 문서(곧 프린트 될 문서) 보다 우선 순위가 앞선 문서가 있으면, 곧 프린트 될 문서를 큐에 끝으로 보낸다.

<br/>
<br/>

## 풀이
---
* 프린트 될 문서의 정보(몇번째로 출력될 지 알고 싶은 문서, 우선순위)를 담기 위해 'Print' 객체 생성
* 큐 가장 앞에 있는 문서(now-doc 이라고 하겠다)가 출력이 되려면 우선순위가 뒤에 문서들 보다 높아야 함
* now-doc 이 출력 되면 큐에서 poll 해주고 남은 문서로 출력 될 문서를 찾음
* 큐에서 poll 한 문서를 list 에 담아서 출력된 순서를 저장
* 입력 받은 '몇번째로 출력될 지 알고 싶은 문서'의 번호와 위에 list 를 돌면서 순서를 찾아냄

## Code
---
~~~
package backjoon;

import java.util.*;
import java.util.Queue;

public class PrintQueue {

  public static void main(String[] args) {
    Scanner scan = new Scanner(System.in);

    int tc = scan.nextInt();

    StringBuilder sb = new StringBuilder();

    for (int i = 0; i < tc; i++) {
      int N = scan.nextInt();
      int target = scan.nextInt();

      scan.nextLine();

      String[] numSet = scan.nextLine().split(" ");

      Queue<Print> queue = new LinkedList<>();

      for (int k = 0; k < N; k++) {
        queue.offer(new Print(k, Integer.parseInt(numSet[k])));
      }

      int result = PrintQueue.resultOrder(target, queue);

      sb.append(result);
      sb.append("\n");
    }

    System.out.println(sb.toString());
  }

  private static int resultOrder(int target, Queue<Print> queue) {
    int result = 0;

    List<Print> resultPrint = new ArrayList<>();

    int qSize = 0;

    while ((qSize = queue.size()) != 0) {
      boolean orderFlag = true;

      qSize = queue.size();

      if (qSize != 1) {

        Print nowDoc = queue.peek();
        int nowDocPri = nowDoc.getPriority(); // 가장 앞에 있는 문서

        Iterator<Print> qIter = queue.iterator();

        while (qIter.hasNext()) {
          Print nextPrint = qIter.next();
          int nextDocPri = nextPrint.getPriority();

          if (nextDocPri > nowDocPri) {
            queue.poll();
            queue.offer(nowDoc);

            orderFlag = false;

            break;
          }
        }
      }

      if (orderFlag) {
        resultPrint.add(queue.poll());
      }
    }

    int listSize = resultPrint.size();

    for(int i = 0; i < listSize; i++) {
      Print p = resultPrint.get(i);

      if(p.getOrder() == target) {
        result = (i + 1);
        break;
      }
    }

    return result;
  }

  static class Print {
    private int order;
    private int priority;

    public Print(int order, int priority) {
      this.order = order;
      this.priority = priority;
    }

    public int getOrder() {
      return this.order;
    }

    public int getPriority() {
      return this.priority;
    }
  }
}
~~~