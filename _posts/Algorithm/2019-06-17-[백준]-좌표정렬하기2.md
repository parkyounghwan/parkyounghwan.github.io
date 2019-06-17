---
layout: post
title:  "[백준] 좌표 정렬하기2"
date:   2019-06-17
categories: Algorithm
comments: false
---

## 문제 요약
---
링크 : [좌표 정렬하기2](https://www.acmicpc.net/problem/11651)  

> 2차원 평면 상에 좌표(x, y)가 주어진다. 좌표를 y 값의 오름차순으로 정렬하고, y 값이 같을 경우, x 값의 오름차순으로 정렬하라.  
1. 좌표가 같은 경우, 중복 되는 경우는 없다.

## 풀이
---
Java 에서는 정렬 메소드를 지원한다.

Collections 클래스에서 제공하는 sort() 는 Comparator와 Comparable 에서 구현하고 있다.  

따라서, 정렬 기준에 따라 _Comparator_ 혹은 _Comparable_ 의 compare 메소드를 오버라이드 해서 커스텀 한 정렬을 구현 할 수 있다.

위 문제에서는 정렬 조건이 2가지 있다.
1. 각 Point 들을 y 값의 오름차순으로 정렬한다.
2. 정렬하다가 같은 y 값일 경우, x 값으로 오름차순을 진행한다.

_Comparator_ , _Comparable_ 아무 방식이나 사용해도 괜찮다.

> 여기서, 백준에서 풀었을 때, 나는 _Wrapper Class_ , Integer 타입으로 Point 객체를 구현했었는데 틀렸다고 나왔다. 멤버 변수를 Primitive Type 으로 구현 할 것을 추천.

## Code
---
~~~
package backjoon;

import java.util.*;

public class PointSort2 {

  static class Point implements Comparable<Point>, Comparator<Point> {
    int x, y;

    public Point() {
    }

    public Point(int x, int y) {
      this.x = x;
      this.y = y;
    }

    @Override
    public int compareTo(Point o) {
      if (this.y > o.y) {
        return 1;
      } else if (this.y == o.y && this.x > o.x) {
        return 1;
      } else if (this.y == o.y && this.x < o.x) {
        return -1;
      } else if (this.y < o.y) {
        return -1;
      }

      return 0;
    }

    @Override
    public int compare(Point o1, Point o2) {
      if(o1.y == o2.y) return (o1.x > o2.x) ? 1 : -1;
      else return (o1.y > o2.y) ? 1: -1;
    }

    @Override
    public String toString() {
      return this.x + " " + this.y;
    }
  }

  public static void main(String[] args) {
    Scanner scan = new Scanner(System.in);

    int T = scan.nextInt();

    List<Point> list = new LinkedList<>();

    for (int i = 0; i < T; i++) {
      int x = scan.nextInt();
      int y = scan.nextInt();

      list.add(new Point(x, y));
    }

    Collections.sort(list, new Point());

    for (Point point : list) {
      System.out.println(point.toString());
    }
  }
}
~~~