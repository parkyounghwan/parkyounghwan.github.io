---
layout: post
comments: false
categories: mysql
---
  
### 문제 상황
> 인덱스가 걸려 있는 컬럼을 GROUP BY를 사용하여 조회하는데, 속도가 나오질 않는다.

    
## GROUP BY 란?
'GROUP BY' 절은 동일한 값을 가진 데이터를 [집계](https://ko.dict.naver.com/#/entry/koko/a13a75d37c87458d8aa5b0fcd15b6e80)해서 조회하고자 할 때 사용하는 문장이다. 

### 작성 방법
* 집계 할 칼럼을 'GROUP BY' 절 뒤에 적어준다.
* 'SELECT' 절에는 'GROUP BY' 절에 명시된 칼럼만 사용할 수 있다.
 
~~~
SELECT colume_A
FROM table_A
GROUP BY column_A
~~~

### 이해
* 조회되는 데이터의 동일한 값들을 하나의 데이터로 집계하는 문장. 
 
> 학교에서, '학생 이름'을 GROUP BY 절을 사용해서 출력한다고 하면, 같은 이름이 여러번 출력되지 않고, 각 이름 하나씩 집계되어 출력된다. 
(ex, 학교에 '박영환' 이라는 동명이인이 많을 텐데, 이런 이름 종류를 하나씩만 출력) 
 
~~~
SELECT 이름
FROM 학교
GROUP BY 이름
~~~
 

__'GROUP BY' 와 집계 함수의 사용__
* `집계 함수`는 'GROUP BY' 절에 표시된 컬럼들에 집계한 결과값을 만들어 준다. 
* 'GROUP BY' 절에 표시하지 않은 컬럼도 `집계 함수`를 사용하면 SELECT 절에 사용이 가능하다. 

> 학교에 '박영환'이 몇명 있는지 출력할 떄. 
 
~~~
SELECT 이름, COUNT(*) as 인원
FROM 학교
GROUP BY 이름
~~~
 
 
## GROUP BY 최적화
* __GROUP BY 절은 테이블을 스캔하고 결과를 임시 테이블에 넣어서 집계하는 과정을 거친다.__ 
    * 따라서, 데이터 양이 많으면 매우 느린 쿼리가 될 수도 있다. 그래도 인덱스를 잘 설정한다면 '임시 테이블'을 생성하지 않고 빠르게 데이터를 가져올 수 있다.   
    * *관건은 GROUP BY 에 있는 모든 컬럼들이 바라보는 INDEX가 동일하고 순서도 맞아야 한다.*  

* __GROUP BY 를 빠르게 하기 위해서는 GROUP BY 에 사용된 컬럼 값으로 정렬이 되어 있어야 한다.__  
    * GROUP BY 는 동일한 값을 동일한 그룹으로 묶겠다는 것이므로, 정렬이 되어 있으면 그 자체로 그룹핑이 완료되었기 때문이다.  
    * 필요하다면, 정렬을 위해 GROUP BY 에 사용되는 컬럼을 INDEX로 생성해야 한다.  
  


{% highlight lua %}
SELECT A.*, COALESCE(SUM(B.count),0) as count 
FROM sgRNA_1 AS A LEFT OUTER JOIN offtargets_1 AS B ON A.sgRNA_ID = B.sgRNA_ID
WHERE ((A.c >= 758454.9288256228 AND A.c <= 759504.9288256228)) 
GROUP BY sgRNA_ID; 
{% endhighlight %}
: COALESCE() - ‘null’ 체크 함수, COALESCE(param1, param2) => ‘param1’이 ‘null’ 일 경우 ‘param2’의 값으로 대체한다. 
: ‘B’ 는 ‘offtarget_1’ 테이블, 해당 테이블의 count 칼럼은 row의 특정한 상수를 나타냄. 
 
: 일반 ‘JOIN(INNER JOIN)’ 시에는 pk, fk에 상응하는 값이 없으면 row 조차 출력되지 않음, 같은 조건이 있으면 모조리 출력. 
=> 예를들어 A 테이블의 한 ROW의 PK와 상응하는 B 테이블의 ROW가 3개가 존재하면 3개가 모두 매핑되서 출력. 
 
: ‘LEFT & RIGHT JOIN(LEFT & RIGHT OUTER JOIN)’ 의 경우, 기준되는 테이블, 반드시 출력되야하는 테이블을 잡아준다. (매핑되는 결과가 없더라도 기준되는 테이블의 칼럼은 최소한 1줄은 보장 받는다) 
=> 위와 같은 예에서 A 테이블에 B 테이블 FK에 상응하는 ROW가 없는 경우 최소한 1줄이 출력된다. 위와 동일하게 매핑되는 ROW가 3개가 존재하면 3개 다 출력. 
 
: 만약 해당 범위에 대한 A 테이블의 갯수가 100개가 나온다면, 최소 100줄은 나와야 한다. 
 
: 문제 지점이다, 해당 쿼리 절에 인덱스를 걸어줘야하는데 어떤 테이블의 인덱스를 걸어줘야 데이터 정합성에 위배되지 않고 결과를 출력할 수 있을 것인가. 
: 또, 만약, A 테이블의 인덱스로 사용할 경우, 이미 A 테이블에서 인덱스 검색을 사용(WHERE 절)하고 있는데, 두개의 인덱스를 MySQL이 소화 할 수 있는지.
~~~

