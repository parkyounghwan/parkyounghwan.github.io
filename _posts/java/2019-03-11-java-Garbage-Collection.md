---
layout: post
title: "Garbage Collection"
date:   2019-03-11
comments: false
categories: Java
---
참고: [Naver, D2 - Garbage Collection](https://d2.naver.com/helloworld/1329)  

## Garbarge Collection
> GC 과정에 관심을 가잘 정도라면 규모가 일정 이상인 애플리케이션을 제작해 본 경험이 있을 것이라는 전제가 깔린다. 또한 어떤 GC 알고리즘을 선택할 것인지 고민할 수 있다는 것은 제작한 애플리케이션의 특징을 정확히 이해 했다는 반증이다.  
  
*간략하게 말하자면, GC란 Java 에서 쓰이지 않는 객체를 모아서 메모리를 관리하는 기술*  
  
### 가비지 컬렉션 과정
* __`stop-the-world`__
    * GC 를 실행하기 위해, JVM이 애플리케이션 실행을 멈추는 것.
    * `stop-the-word` 가 발생하면 GC를 실행하는 쓰레드를 제외한 나머지 쓰레드는 모두 작업을 멈춘다. GC 작업을 완료한 후에 중단했던 작업을 다시 시작한다.
    * 대개의 경우 GC 튜닝이란 이 `stop-the-world` 시간을 줄이는 것이다.
  
Java는 프로그램 코드에서 메모리를 명시적으로 지정하여 해제하지 않는다. 가끔 명시적으로 해제하려고 해당 객체를 null로 지정하거나 System.gc()를 호출하는데, null로 지정하는 것은 큰 문제가 되지 않지만, System.gc()를 호출하는 것은 시스템의 성능에 매우 큰 영향을 미친다.  
  
Java에서는 개발자가 프로그램 코드로 메모리를 명시적으로 해제하지 않기 때문에 가비지 컬렉터가 더 이상 필요 없는 객체를 찾아 지우는 작업을 한다. C의 경우 메모리 할당 해제를 코드 상에서 처리한다.  
  
가비지 컬렉터는 아래 두 가지 전제(?), 가설(?) 하에 만들어 졌다.
> * 대부분의 객체는 금방 접근 불가능 상태(unreachable)가 된다.
* 오래된 객체에서 젊은 객체로의 참조는 아주 적게 존제한다.

이러한 가설을 'week generation hypothesis' 라 한다. 이 가설의 장점을 최대한 살리기 위해 HotSpot VM에서는 크게 2개로 물리적 공간을 나누었다. 둘로 나눈 공간이 `Young 영역` 과 `Old 영역` 이다.  

* `Young 영역` (Young Generaion 영역)  
    * 새롭게 생성한 객체의 대부분이 여기에 위치한다. 대부분의 객체가 *금방 접근 불가능 상태* 가 되기 때문에 매우 많은 객체가 `Young 영역` 에 생성되었다가 사라진다.  
    * 이 영역에서 객체가 사라질때 __Minor GC__ 가 발생한다고 말한다.  
* `Old 영역` (Old Generation 영역)
    * __접근 불가능 상태로 되지 않아 Young 영역에서 살아남은 객체가 여기로 복사된다.__
    * 대부분 Young 영역보다 크게 할당하고, 크기가 큰 만큼 Young 영역보다 GC는 적게 발생한다.
    * 이 영역에서 객체가 사라질 때 __Major GC 혹은 Full GC__ 가 발생한다고 말한다.  

그렇다면 __"Old 영역에 있는 객체가 Young 영역의 객체를 참조하는 경우가 있을 때, 어떻게 처리될까?"__ 라고 궁금해 하는 분도 더러 있을 것이다. 이러한 경우를 처리하기 위해서 `Old 영역`에는 512바이트의 덩어리로 되어있는 카드 테이블(card table)이 존재한다.  
  
카드 테이블에는 `Old 영역`에 있는 객체가 `Young 영역`의 객체를 참조 할 때마다 정보가 표시된다. `Young 영역`의 GC를 실행할 때에는 `Old 영역`에 있는 모든 객체의 참조를 확인하지 않고, 이 카드 테이블만 뒤져서 GC 대상인지 식별한다.  




