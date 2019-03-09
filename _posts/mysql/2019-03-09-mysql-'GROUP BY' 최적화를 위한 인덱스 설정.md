---
layout: post
comments: false
categories: mysql
---
  
문제 상황
> 인덱스가 걸려 있는 컬럼을 GROUP BY를 사용하여 조회하는데, 속도가 나오질 않는다.


__GROUP BY 절은 테이블을 스캔하고 결과를 임시 테이블에 넣어서 집계하는 과정을 거친다.__  
따라서, 데이터 양이 많으면 매우 느린 쿼리가 될 수도 있다. 그래도 인덱스를 잘 설정한다면 '임시 테이블'을 생성하지 않고 빠르게 데이터를 가져올 수 있다.  
*관건은 GROUP BY 에 있는 모든 컬럼들이 바라보는 INDEX가 동일하고 순서도 맞아야 한다.*  

__GROUP BY 를 빠르게 하기 위해서는 GROUP BY 에 사용된 컬럼 값으로 정렬이 되어 있어야 한다.__  
GROUP BY 는 동일한 값을 동일한 그룹으로 묶겠다는 것이므로, 정렬이 되어 있으면 그 자체로 그룹핑이 완료되었기 때문이다.  
필요하다면, 정렬을 위해 GROUP BY 에 사용되는 컬럼을 INDEX로 생성해야 한다.  
  
~~~
SELECT A.*, COALESCE(SUM(B.count),0) as count  
FROM sgRNA_1 AS A LEFT OUTER JOIN offtargets_1 AS B ON A.sgRNA_ID = B.sgRNA_ID  
WHERE ((A.c >= 758454.9288256228 AND A.c <= 759504.9288256228))  
GROUP BY sgRNA_ID;  
~~~

