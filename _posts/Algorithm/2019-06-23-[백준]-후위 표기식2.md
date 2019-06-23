---
layout: post
title:  "[백준] 후위 표기식 2"
date:   2019-06-23
categories: Algorithm
comments: false
---

## 문제 요약
---
링크 : [후위 표기식 2](https://www.acmicpc.net/problem/1935)  

> 후위표기식으로 주어지는 문자열을 계산해라. 표기식에서 피연산자는 알파벳으로 표현되고, 각 알파벳에 맞는 숫자가 주어진다.

<br/>
<br/>

## 풀이
---
후위 표기식 자체는 연산자 뒤에 나오는 두 피연산자에 대한 계산만 해주면 어려운 문제는 없는데, 문자열 자체로 주어지는 연산자와, 피연산자를 분리하고, 적절하게 피연산자에 대한 숫자를 매칭해주는 부분만 잘 처리해주면 될 것 같다.

<br/>

예를들어, 피연산자가 'ABC' 로 주어지면 매칭 되는 숫자는 '3', '12', 8' 등으로 주어진다. 순서대로 매칭을 해주면 되어서, 배열에 매칭되는 숫자를 넣고. 알파벳을 _char_ 형으로 변환 한 후에 _'a'_ 를 빼서, 인덱스에 맞는 숫자를 매핑해 주었다.

<br/>

문자열에서 알파벳과 연산자('+', '-', '*', '/') 를 구별해 내야 하는데 정규표현식을 사용해서 구별했다.

### 정규 표현식
---
~~~
public static String getType2(String word) {

    Pattern alphaPattern = Pattern.compile("^[a-z]*$");
    Pattern numberPattern = Pattern.compile("^[0-9]*$");
    Pattern operatorPattern = Pattern.compile("[ !@#$%^&*(),.?\":{}|<>]");

    Matcher alphaMatcher = alphaPattern.matcher(word);
    Matcher numberMatcher = numberPattern.matcher(word);
    Matcher operatorMatcher = operatorPattern.matcher(word);

    String result = null;

    if(alphaMatcher.matches()) result = "alphabat";
    if(numberMatcher.matches()) result = "number";
    if(operatorMatcher.matches()) result = "operator";

    return result;
  }
~~~

* Pattern 클래스로 어떤 패턴을 골라낼 건지 정규 표현식을 입력한다.
* Matcher 클래스에는 결과를 담는데, Pattern 클래스의 matcher 메소드로 검사하고자 하는 문자열을 검사한 결과를 Matcher에 담아서 사용했다.
* 위에는 '알파벳(소문자)', '숫자', '특수문자' 를 구별해 보고자 여러 정규 표현식을 써봤다.

<br/>
<br/>

## Code
---
~~~
package backjoon;

import java.util.*;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class PostfixExpression2 {

  private static final Scanner scan = new Scanner(System.in);

  public static boolean getType1(String word) {
    return Pattern.matches("^[a-z]*$", word);
  }

  public static void main(String[] args) {
    int N = scan.nextInt();
    scan.nextLine();

    String pe = scan.nextLine();

    int[] val = new int[N];
    for (int i = 0; i < N; i++) {
      val[i] = scan.nextInt();
    }

    Stack<String> stack = new Stack<>();
    Set<String> componentSet = new HashSet<>();
    componentSet.add("+");
    componentSet.add("-");
    componentSet.add("/");
    componentSet.add("*");

    double result = 0;

    for (String ele : pe.split("")) {

      if (componentSet.contains(ele)) {

        String b = stack.pop().toLowerCase();
        String a = stack.pop().toLowerCase();

        double bIdx = !getType1(b) ? Double.valueOf(b) : val[(b.charAt(0) - 'a')];
        double aIdx = !getType1(a) ? Double.valueOf(a) : val[(a.charAt(0) - 'a')];

        switch (ele) {
          case "+":
            result = (aIdx + bIdx);
            break;
          case "-":
            result = (aIdx - bIdx);
            break;
          case "*":
            result = (aIdx * bIdx);
            break;
          case "/":
            result = (aIdx / bIdx);
            break;
        }

        stack.push(String.valueOf(result));

      } else {

        stack.push(ele);

      }

    }
    System.out.println(String.format("%.2f", result));
  }
}

~~~