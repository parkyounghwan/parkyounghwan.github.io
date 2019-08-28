---
layout: post
title:  "Git 에서 IDE 로, IDE 에서 Git 으로 연동 2"
date:   2018-09-14 
categories: Github
comments: false
---

### 회상 
~~~
잊어먹을까봐 간략히 정리해 논다.

1. STS에 깃 저장소 등록해 놓고, 프로젝트 쉐어 하고 커밋했는데 프로젝트 통짜로 올라감 개빡침, 폴더 눌러보고 별 짓 다 해봤는데 무조건 통짜로 밖에 안올라감.

(지금 생각해보니까, 저장소 등록을 역으로 하면 될 수도 있을 거 같은 느낌인데, 다음에 해본다)

2. 그래서 그냥 로컬 저장소에 프로젝트 폴더 복사해서 쓰다가, 아무리 생각해도 이건 IDE를 쓰는 이점이 없는 그지 같은 상황이 비관스러웠음.

3. 또 그래서, Git에 올려놓은 내 프로젝트를 IDE(STS)에 import 시켜서 연결하자고 마음먹음.

4. 근데 내가 겉멋이 들어서 .gitignore 로 필요없는 파일들을 다 제외 시켜놨음. 그래서 안됨.

5. 근데 또, 생각해 보니까 아니 그럼 내 프로젝트 폴더에 숨김 파일 까지 모조리 로컬 저장소에 올리면 왠지 될거같은 느낌이 들었음.

6. 그래서 숨김파일 까지 싹다 로컬에 올리고, 리소스 파일 이런건 빼고 깃에 푸쉬함.

7. 깃 보니까 뭔가 형식을 갖춰서 올라갔음.

8 그리고 나서 이제 그 원격 저장소를 내 IDE에 연결시키면 나는 바로바로 내가 수정한 파일만 굳이 고르지 않아도 확인하지 않아도 커밋이 가능하게 된다는 부푼 희망을 가졌음.

9. 그래서 그걸 했음. tobecontinue
~~~

  

### GitHub Repository 와 STS project 연결하기
---
STS or Eclipse 에서 git 최대한 활용하기.

  1. GitHub Repository 만들기.  
  'GitHub' 사이트에서 레포 만들고, git clone '원격저장소 주소' 하면 생긴다. 따로 설명 안한다.
  
  2. 프로젝트의 모든 파일 복사.  
  _STS에서 본 프로젝트 구조_
  ![](https://t1.daumcdn.net/cfile/tistory/99847F375B9B42FA2B)
  
  - spring boot 프로젝트이고, 무슨 프로젝트인지는 상관없다.  
  - git에는 대게 소스코드만 올리고 설정파일 등은 올리지 않는다.
  - 거의 'src' 폴더, 'pom.xml' 정도만 올린다.
  - 하지만 난 일단 싹 다 올릴 것이다.


### terminal 로 본 프로젝트 구조. (_'ls -al'_ 로 숨김 파일까지 모조리 본다)
---
![](https://t1.daumcdn.net/cfile/tistory/9992864A5B9B447F1A)
- 이거 전체 복사해서 1번에서 만든 원격저장소에 때려 박는다.
- 터미널 명령어는 => '$ cp 해당폴더/* 옮길폴더/' 
- 해당 폴더는 STS workspace 안에 본인 프로젝트가 될 거고, 옮길 폴더는 원격 저장소 폴더가 될 것이다.
- '*' 모든 폴더 및 파일 옮기겠다는 것.
- 주의) 폴더 자체를 옮기면 이렇게 할 필요 없다. 우리는 GitHub Repository에 내 프로젝트의 구조를 맞추려는 것이다. => commit 시에 폴더 자체가 add 되지 않게 하기 위해서. 


### 빼고 올리는 방법
---
> '-r' 은 폴더일 경우이다.

1. 원격 저장소에서도 삭제하고 올리고 싶은 경우.  
$ git rm '삭제하고 싶은 파일, 디렉토리 경로까지 명시해 줘야됨'
  
2. 원격 저장소 폴더에는 남겨두고 commit 시에만 포함 안되게 해주기(빼 놓으면 계속 빠져있음)  
$ git rm --cached '위와 동일'

  - 'git add .' => 'git commit -m "initial commit"' => 'git push origin master'


### STS로 내려 받는다

> **File -> Import -> Git -> Project from Git -> Existing local repository**

![](https://t1.daumcdn.net/cfile/tistory/996C5B3D5B9B4A2309)  

![](https://t1.daumcdn.net/cfile/tistory/994DB83D5B9B4A230C)  

![](https://t1.daumcdn.net/cfile/tistory/99856A3D5B9B4A2407)  
- 우리는 로컬에 원격저장소 폴더가 있으니 그 폴더에 연결하는 것이다.
- 폴더 자체에 이미 우리 프로젝트에 골격이 다 있기 때문에 import만 하면 되는 것.

### git repository에서 내려받은 프로젝트 sts에 import 할 때 주의할 점
---
뭐냐면, 나의 경우에는 pom.xml 에 추가한 라이브러리들을 프로젝트가 읽지 못하는 경우가 발생하였다. 더 쉽게 말해서, ‘import org.springframework.~’ , ‘import lombok.~’ 등등의 라이브러리 코드를 읽지를 못하는 상황, 어노테이션도 읽지를 못함. 보니까 maven dependency가 올바르게 처리되지 못한 경우에 이런 에러가 발생한다고 함. (tomcat의 server plugin의 임시 deploy 디렉토리에 WEB-INF/lib에 jar들이 정상 배포되지 않기 때문.. 톰켓..)

해결 방법은 아래 블로그에 나와 있다.  

* [Maven 환경의 프로젝트 구동시 에러](http://arcsit.tistory.com/entry/ERROR-Maven-%ED%99%98%EA%B2%BD%EC%9D%98-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EA%B5%AC%EB%8F%99%EC%8B%9C-%EC%97%90%EB%9F%AC)


