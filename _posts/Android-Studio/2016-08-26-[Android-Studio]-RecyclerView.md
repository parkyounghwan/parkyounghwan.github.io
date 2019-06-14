---
layout: post
title:  "[Android-Studio] RecyclerView"
date:   2016-08-26 
categories: Android-Studio
comments: false
---

## RecyclerView를 사용하여 뉴스피드 형식의 앱 만들기.  
---

### 뉴스피드 형식의 View 만들기
뉴스피드 : 새로운 소식(news)가 흐르는(feed) 곳

#### 1. RecyclerView 지정하기  
---

- RecyclerView가 기본 라이브러리가 아니어서 다운을 받아와야 한다.
- 프로젝트 폴더 우클릭 후 **'Open Module Settings'** 클릭.  
![](https://t1.daumcdn.net/cfile/tistory/2403FA4057C7D15A1A)



- 사이드 바 하단에 'app' 클릭 -> 상단 바에 'Dependencies' 클릭 -> 하단에 '+' 클릭 후 첫번째 항목 'Library dependency' 클릭.  
![](https://t1.daumcdn.net/cfile/tistory/277D294657C7D19B07)
    > 나는 이미 몇개를 추가한 상태여서 다르게 보일 수 있다.  


- 'recyclerview' 검색 후 OK.  
![](https://t1.daumcdn.net/cfile/tistory/2619FA4057C7D28410)

  
- 'build.gradle'에서 적용된 모습 확인.  
![](https://t1.daumcdn.net/cfile/tistory/22151C4A57C7D4AC1B)
    > 위에 보이는 'cardview', 'glide', 'loopj' 같은 것도 동일하게 적용시키면 된다.  


#### 2. 레이아웃 잡기
---

- 두개의 레이아웃이 필요한데 하나는 'RecyclerView'를 적용시키는 'main' view 하나와 recyclerview 각각의 

- item에 들어갈 'Item' view 하나.  

    _'activity\_main'_  
    ![](https://t1.daumcdn.net/cfile/tistory/2420DE3457BFAD3E12)


    _'activity\_item'_  
    ![](https://t1.daumcdn.net/cfile/tistory/25740A4F57C7D82A3B)

    > 빨간 부분 : profile image
    > text 부분 : ID
    > content 부분 : 내용
    > content 하단 부분 : content image  


- 'activity\_main'  
좀 있다가 java코드에서 recyclerview 불러와야 하니 이름 정해주고, 사이즈 꽉 차게 정해준다.

- 'activity\_item'  
전체 레이아웃은 수직으로 배치하였고 상단에 프로필 이미지와 ID부분은 따로 수평 배치하여 레이아웃을 잡았다.  

> item 레이아웃의 경우 본인이 원하는 방식으로 만들어도 되겠다.
  


  


  


  


  


  


