---
layout: post
title:  "[Android-Studio] ListView (미완성)"
date:   2016-09-02 
categories: Android-Studio
comments: false
---

## ListView를 사용해서 전화번호 목록 만들기  
---
### 1. 레이아웃 잡기.
- 'item'으로 쓸 레이아웃.
![](https://t1.daumcdn.net/cfile/tistory/256F323357C9046001)
    > 이 놈을 이제 ListView에 넣어서 쭉쭉쭉 보여 줄 것이다.

  
- ListView를 설정하자 _'activity\_main'_ 이다.
![](https://t1.daumcdn.net/cfile/tistory/2419BE3757C905062C)
    > 그냥 가볍게 원래 있던 'TextView' 지워주고 'ListView' 로 넣어주면 된다.  


- 코드를 보자.
가운데 'ListView' 부분만 바꿔주었다.

- ListView에 있는 item들에 넣어줄 레이아웃 잡아주자. 
_'activity\_item'_ 이라고 새로 하나 만들어 준다. _'activity\_item'_ 이다.
![](https://t1.daumcdn.net/cfile/tistory/256F323357C9046001)
    > 좌측 빈칸 : 이미지 넣을 자리  


- 코드 보자.
전체 'LinearLayout' 은 수평배치(horizontal) 하였고 이미지 넣을 자리 옆으로는 따로 수직배치(vertical)을 주었다.

> 레이아웃 끝
---
  

### 2. java코드 짜기.  

- 'activity\_main' 에 있는 ListView 부터 불러와 보자꾸나. 아 Adapter도 같이 불러보자.  

- 빨간줄 뜨고 난리가 났을텐데 'ListViewAdapter'는 클래스 따로 만들어 주던가 'MainActivity'에서 만들어 주든가 하면 사라지고, 아직 Adapter 객체 생성 안되서 그런거다. 복잡한데 'ListViewAdapter' 클래스만 만들면 문제 해결된다.

- 만들자 'ListViewAdapter', 나는 따로 빼서 만들겠다. 클래스 하나 더 만들자 _'ListViewAdapter'_

- 클래스 이름 뒤에 'extends BaseAdapter' 넣어주고 자동 생성으로 Adapter 메소드들 호출하면 빨간줄 사라진다.

- 데이터도 새로 정의한 클래스로 확장되었고 ListView 아이템도 여러 위젯으로 구성되죠. 이에 따라 Adapter 기능도 확장해야 합니다.

- Adapter를 새롭게 구현할 때 안드로이드 SDK 에서 제공하는 Adapter 중 어떤 Adapter 클래스를 부모로 사용할 지 결정해야 합니다. 본인이 구현하고자 하는 

- Adapter의 기능에 적합한 것을 선택하면 되는데 보통 ArrayAdapter 또는 BaseAdapter를 많이 사용합니다. 일단 예제에서는 BaseAdapter를 사용하겠습니다.
(참고. http://recipes4dev.tistory.com/43)

![](https://t1.daumcdn.net/cfile/tistory/2752733757C90B0E1D)
> 저거 눌러주면 된다.  


  


-생긴 메소드들 한번 보고 넘어가자.

  


 

  


