---
layout: post
title:  "HashMap 은 어떻게 동작하는가"
date:   2018-12-04 
categories: Java
comments: false
---
! NAVER D2 [Java HashMap 은 어떻게 동작하는가?] 를 바탕으로 작성하였습니다.

<https://d2.naver.com/helloworld/831311>

  


  


HashMap 은 Java Collections Framework 에 속한 구현체 클래스.

Map 인터페이스 자체는 Java 5 에서 Generic 이 적용된 것 외에 처음 선보인 이후 변화가 없지만, HashMap 구현체는 성능을 향상시키기 위해 지속적으로 변화해 왔다.

  


  


HashMap 과 HashTable

HashTable 또한 Map 인터페이스를 구현하고 있기 때문에 제공하는 기능은 같지만, HashMap 은 보조 해시 함수를 사용하기 때문에 HashTable 에 비하여 해시 충돌이 덜 발생할 수 있어 상대적으로 성능상 이점이 있다.   


  


HashMap 과 HashTable 을 정의한다면, **'키에 대한 해시 값을 사용하여 값을 저장하고 조회하며, 키-값 쌍의 갯수에 따라 동적으로 크기가 증가하는 associate array' **라고 할 수 있다.

  


# 'associate array'

: 다른 용어로는 'Map', 'Dictionary', 'Symbol Table' 등이 있다.

  


map(or mapping) 은 원래 수학 함수에서의 대응 관계를 지칭하는 용어로, 경우에 따라서는 함수 자체를 의미하기도 한다. key 집합인 정의역과 value 집합인 공역의 대응에 함수를 이용한다.

  


  


해시 분포와 해시 충돌  
동일하지 않은 어떤 객체 X, Y 가 있을 때, 즉 X.equals(Y) 가 '거짓'일 때, X.HashCode() != Y.hashCode() 가 같지 않다면, 이때 사용하는 해시 함수는 '완전한 해시 함수' 라고 한다.  


  


HashMap 은 기본적으로 각 객체의 hashCode() 메서드가 반환하는 값을 사용하는 데, 결과 자료형은 int 이다. 32 비트 정수 자료형으로는 완전한 자료 해시 함수를 만들 수 없다. 논리적으로 생성 가능한 객체의 수가 2의 32 제곱 보다 많을 수 있기 때문이며, 또한 모든 HashMap 객체에서 O(1)을 보장하기 위해 랜덤 접근이 가능하게 하려면 원소가 2의 32 제곱인 배열을 모든 HashMap이 가지고 있어야 하기 때문이다.

  


따라서 HashMap 을 비롯한 많은 해시 함수를 이용하는 associative array 구현체에서는 메모리를 절약하기 위하여 실제 해시 함수의 표현 정수 범위 |N| 보다 작은 M 개의 원소가 있는 배열만을 사용한다. 따라서 다음과 같이 객체에 대한 해시 코드의 나머지 값을 해시 버킷 인덱스 값으로 사용한다.

  


# 해시를 사용하는 associative array 구현체에서 저장/조회할 해시 버킷을 계산하는 방법

int index = X.hashCode() % M;

  


위 코드와 같은 방식을 사용하면, 서로 다른 해시 코드를 가지는 서로 다른 객체가 1/M 의 확률로 같은 해시 버킷을 사용하게 된다. 이는 해시 함수가 얼마나 해시 충돌을 회피하도록 잘 구현되었느냐에 상관없이 발생할 수 있는 또 다른 종류의 해시 충돌이다. 이렇게 해시 충돌이 발생하더라도 Key-Value 쌍 데이터를 잘 저장하고 조회할 수 있게 하는 방식에는 대표적으로 두 가지가 있는데, 하나는 Open Addressing 이고, 다른 하나는 **Separate Chaining** 이다. 이 둘 외에도 해시 충돌을 해결하기 위한 다양한 자료 구조가 있지만, 거의 모두 이 둘을 응용한 것이라고 할 수 있다.

  


![](https://t1.daumcdn.net/cfile/tistory/99B02F4E5C06147513)

  


Open Addressing 은 데이터를 삽입하려는 해시 버킷(위에 배열 인자 하나 하나)이 이미 사용 중인 경우, 다른 해시 버킷에 해당 데이터를 삽입하는 방식이다. 데이터를 저장/조회 할 해시 버킷을 찾을 때에는 Linear Probing, Quadratic Probing 등의 방법을 사용한다.

  


# Linear Probing  
: Linear 한 배열에 Value 를 추가 할 때(위 사진에 'Open Addressing' 같은 배열), 추가되는 index 에 대해 충돌(중복, 이미 사용중인 인덱스, 값이 할당 된 인덱스 등으로 생각)이 발 생할 경우 해당 인덱스 뒤(예를 들어 index '5' 에 value 를 저장하려 했을 때 index '6' 이 뒤 가 된다)에 값을 추가하는 방식.

  


![](https://t1.daumcdn.net/cfile/tistory/99B541395C06173315)

위 그림에서는 해쉬 함수가 index '11' 에 대해서 '1' 의 Hash Kay 값을 반환하므로 '1' 뒤에 남은 공간인 HashTable 에 index '3' 에 값이 위치하게 된다.  


검색의 경우 HashTable 에서 'key' 값이 일치하는지 확인한 후 그 아래로 'key' 가 나오거나 없을 때 까지 검색하게 된다.

  


: 삭제의 경우, 아래 그림의 경우 처럼 중간에 값이 사라지면서 검색이 끊길 수 있다. 이를 방지 하기 위해 값 삭제 시 Dummy Node 를 삽입하여 검색 시 다음 노드 까지 검색을 이어주는 역할을 한다. Dummy Node 를 사용하여 삭제를 진행할 경우 삭제가 빈번히 일어나는 상황이라면 의미 없는 Dummy Node가 계속 쌓이므로, Dummy Node 의 갯수가 일정 양을 넘어가면 새로운 Array 로 Hash 를 Re-Building 해주어야지 성능에 영향을 덜 미칠 수 있다.

  


![](https://t1.daumcdn.net/cfile/tistory/9980F83B5C061A581E)

  


! 조대협의 블로그 - [해시테이블의 이해와 구현(HashTable)] , <http://bcho.tistory.com/1072>

  


