---
layout: post
title:  "[GitHub] Fork 한 Repo, 원본 Repo 와 동기화"
date:   2019-06-19 
categories: Github
comments: false
---

협업을 하면서, 내 Repository 에 프로젝트를 올려서 관리하면 branch 만 달리해서 관리하면 되지만, 상대방의 Repository 에 프로젝트가 올라가 있다면, 내 Repository 에 fork 를 한 후 해당 GitHub Repository 를 clone 받아서 로컬에서 개발 할 수 있다.  

개발을 하던 중에 원본 Repository 가 변경 된다면 어떻게 해야할까. 내가 fork 를 한 Repo 가 원본을 트래킹하고 있는게 아니라 특정 시점에 한 부분을 fork 한 것 이기 때문에, 수동으로 원본 Repo 의 업데이트 된 부분을 맞춰 줘야 한다.

전문 용어로, 원본 Repository 를  _**upstream**_ 이라고 한다.

![Github Upstream-fatch 001](https://user-images.githubusercontent.com/20623970/59767514-7501f100-92dd-11e9-9936-36a9a2219f2c.jpeg)


### 방법

---

어쨌든, _upstream_ 의 Repo 를 내가 fork 한 Repo 로 끌고 와서 동기화를 해줘야 한다.
내 Repo 에는 변경사항이 없다고 가정하고, _upstream_ 의 변경 사항을 동기화 하는 것 이라고 가정한다.



1. 내 로컬의 원격 저장소 (fork 뜬 디렉토리) 에 _upstream_ 의 저장소 주소를 등록한다.

   ~~~terminal
   $ git remote add upstream [원본 저장소 주소]
   $ git remote -v 	// 추가 된 원본 저장소 확인
   ~~~

2. _upstream_ 으로 부터 업데이트 된 내용 불러오기.

   ~~~
   $ git fetch upstream
   ~~~

   _fetch_ 는 단순히 원격 저장소의 내용을 확인만 하는 역할. 
   원격 저장소의 최신 이력을 '확인' 할 수 있다.
   _fetch_ 와 _merge_ 를 합친 것이 _pull_. 

3. _upstream_ 의 원하는 branch 를 선택해서,  나의 소중한 저장소(fork 한 Repo)에 merge 한다.  

   ~~~
   $ git branch -a		           
   $ git checkout master
   $ git merge upstream/master
   ~~~

4. 로컬 저장소에서의 작업을 마쳤으니, GitHub 사이트 (내 원격 저장소) 에 push 를 해 준다.

   ~~~
   $ git push (origin) (master)
   ~~~

![Github Upstream-fetch 003 001](https://user-images.githubusercontent.com/20623970/59767597-97940a00-92dd-11e9-80c9-3911f34ae067.jpeg)
