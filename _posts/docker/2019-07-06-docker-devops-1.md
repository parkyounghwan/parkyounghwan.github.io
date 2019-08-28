---
layout: post
title:  "[Fast Campus] Docker 강의 1"
date:   2019-07-06 
categories: docker
comments: false
---

## Docker 기반 DevOps 인프라 구축 (1)

---

처음엔 쉽게 가다가 뒤로 갈 수록 어려워 진다.
후반부에는 DevOps 와 MSA 관련 내용도 다루게 된다.

<br/>

### 도커에 대한 지식과 경험은 얼마나? / DevOps 에 대한 지식과 경험은 얼마나?

---

서버 운영, 컨테이너, DevOps, 가상화, 미들웨어, RNR

<br/>

### 도커는 무엇인가

---

**리눅스 컨테이너** 기술을 이용해 어플리케이션 **패키징**, **배포**를 지원하는 **경량**의 **가상화** 플랫폼

* 엔진은 Go 언어로 개발
* 최신 버전: v18.09.7 (2019.06.27)
* 엔터프라이즈 급에서 Go Lang 을 많이 도입하고 있다.

<br/>

### 왜 도커를 써야 하나

---

다양한 OS 와 다양한 디바이스에 본인들의 어플리케이션을 올리기 쉽게 하기 위해.

<center>어떤 OS/Device 에서도 동일한 방식으로 배포가 가능</center>

<br/>

### Immutable Infrastructure

---

도커를 사용함으로 _Immutable Infrastructure_ 의 모든 부분을 커버 할 수 있다.

<br/>

### 도커는 왜 성공했을까?

---

리눅스 컨테이너는 소개된지 10년이 지난 기술이지만! 어렵다..

기술 자체나, 설정이 복잡하고 사용하기 어려워서 널리 사용되지 못했다.

그렇다고, 도커가 쉽다고 생각하면 안된다. 강의는 도커의 일부를 가르칠 뿐이고, 여러번 또 여러 군데에 사용하면서 익혀야 한다.

* [The future of Linux containers](https://www.youtube.com/watch?v=wW9CAH9nSLs) - 2013, PyCon

<br/>

#### $ docker run busybox echo 'Hello World'

* 로컬에 busybox 이미지 확인, 없으면 docker hub 에서 다운로드
* busy box 이미지로 새 컨테이너 생성
* 컨테이너 실행
* TTY 로 'Hello World' 출력
* 출력된 결과를 유닉스 소켓을 통해 클라이언트로 전송

=> 리눅스 컨테이너에서, IP 할당하고, 디스크 할당하고, 프로세스를 돌리고 하는 많은 과정을 한번에 정리했다.

<br/>

### 도커 구성요소

---

#### Docker CE 버전 특징

* 무료
* 최신 버전
* 클라이언트 위주 (개발자, 리눅스, 클라우드)

CE 버전만 쓰더라도, 충분하다.

<br/>

#### Swam (Docker, corp) vs Kubernetes (Google)

도커를 깔면, 네이티브 레벨에서 둘 다 깔린다. 뭘 쓰든지 간에 차별 받는 것은 없고, 본인들 한테 유리한 것을 쓰면 된다.

DKS (Docker Kubernetes Service), 쿠버네티스는 구글의 기술인데, DockerCon 2019에서 아예 서비스로 소개를 했다.

<br/>

#### Docker Client

도커 엔진과 통신하는 단말.

<br/>

#### Docker CE for Mac

xyhve /

<br/>

#### Docker Host OS

* 도커 엔진을 설치할 수 있는 환경.
* 리눅스, 64bit  이상

<br/>

#### Docker Engine

어플리케이션을 컨테이너로 만들고 실행하게 해주는 데몬

* Swarm, Kubernetes 와 통합

<br/>

### 윈도우는 도커 호스트 OS 일까?

---

윈도우 레이어 위에 도커를 설치해서, 리눅스를 돌릴 수 있다.

<br/>

### 도커 어디까지 왔나

---

* Docker Conference
  글로벌 스케일로 성장하는 중, DevOps 와 이노베이션의 중심
  * Choice : 클라우드, OS에 종속되지 않는다.
  * Agility : 생산성, 효율증가
  * Security: 어플리케이션으로부터 데이터 분리 (stateless 를 지원)



* 은행권에서도 도입

<br/>

## Docker Architecture

---

가상화라고 하면 하이퍼바이저 라고 한다.

### Hypervisor

---

가상화 머신 모니터, 가상화 머신 에디터

<br/>

TYPE1 과 TYPE2 로 나뉘고, 하드웨어 위에 하이퍼바이저가 올라가서 OS를 만들면 TYPE1 방식이고, 중간에 OS를 끼면 TYPE2 방식.

Docker 는 Host OS 를 빌려쓰기 때문에 가볍다. (TYPE2)

<br/>

#### Linux Container

----

단일 리눅스 호스트상에서 여러개의 격리된 리눅스 시스템을 실행하기 위한 OS 수준의 가상화.

<br/>

#### 클라이언트 환경 변수

---

* 기본적으로 https, 'DOCKER_TLS_VERIFY="1"' ("0", 은 http)
* 도커 클라이언트는 단지 도커 호스트를 바라보기만 하는 것, 호스트의 주소를 바꿀 수 있다. 그 호스트의 인증서만 등록하면 되고, 등록하는 환경 변수 설정도 바꿀 수 있다.

<br/>

#### 기반 기술

---

* Namespace

  프로세스 별 리소스 격리

* Control groups (== cgroups)

  실행중인 어플리케이션이 원하는 만큼 리소스를 사용하게 한다. 특정 컨테이너가 지정한 만큼 리소스를 쓰도록 제한한다.

* Union Filesystem

  다른 파일 시스템을 Union mount 하도록 해주는 리눅스 파일 시스템 서비스.

* 권한 수준
  * root 사용자와 동일한 수준의 권한이 필요. (도커가 리눅스 커널에 접근하기 때문에)
  * TCP 포트가 아닌 Unix 소켓과 데몬이 바인딩 하기 때문 (TCP 포트를 사용하면, 외부에서 커널을 접근 할 수 있다, 해킹의 위험이 있다.)
  * 사용자 그룹 : docker / 사용자 : docker

<br/>

#### 도커 이미지

---

* 컨테이너를 만들기 위한 템플릿

* **읽기 전용 파일 시스템** 으로 도커가 애플리케이션을 배포하는 단위.

* **레이어 파일 시스템** 으로 각 파일 시스템이 곧 이미지.

  'Base Image (Debian)' + 'Image (add emacs)' + 'Image (add Apache)' + 'Container (writable)'   

  한 개의 이미지가 하나의 도커 이미지 일 수도 있고, 여러개의 이미지가 하나의 도커 이미지 일 수도 있다.  

  여러 이미지 중 하나의 이미지에 에러가 나면 사용할 수 없다. (읽기 전용인 이유)

* 컨테이너를 만들기 위해 만들어 놓은 읽기 전용 파일 시스템.

<br/>

##### 베이스 이미지

이미지의 부모가 되는 이미지.

공식 베이스 이미지는 ubuntu 였는데, alpine 으로 변경되었다. 베이스 이미지에 나의 이미지를 쌓아 올려서 도커 이미지를 만들어야 하는데, alpine 은 5 메가 밖에 되지 않는다. 알파인은 에러가 많이 나서, 어렵다. 뺄거 다 뻈기 때문에, 보통은 ubuntu 를 써라.

<br/>

##### 도커는 어떻게 이미지의 변경된 부분만 저장하는가

Git 의 형성관리원리와 같다. (light weight 한 이유)

<br/>

##### Dockerfile

도커 이미지를 만들기 위해 설치할 SW, 필요한 설정을 정의하는 파일

* '#' 주석
* Base Image 명시 : _FROM_
* MAINTAINER : _관리자 info_
* RUN : _명령어 실행_
* EXPOSE : _웹 서비스는 port 로 통신하기 때문에 port 열어 준다_

대소문자 구분 하지 않는다. 

도커 파일을 만드는 이유, **이미지 제작 과정을 투명하게 해야 한다**. DevOps 와 관련된 이야기 인데, 누구든 바꿀 수 있어야 한다.

<br/>

* **Dockerfile Cheat Sheet**

  * EXPOSE : 고개하는 포트를 정의한다.  

    두개를 써야 한다면 ?

    ~~~dockerfile
    EXPOSE 80 443
    ~~~

  * ADD : jar, zip 파일 이라면, 압축을 풀어서 폴더를 만든다.

  * COPY : 폴더를 만들지 않고, 복사만.

  * ENTRYPOINT : 이미지를 여러개 만들기 싫을 때, Node 를 띄워 놓고 프로젝트만 바꿀 때.

  * ONBUILD : 이미지 빌드 후 실행되는 명령. (일반적으로 많이 쓰이지는 않는다. '항상 특정 보안 패키지가 실행되는지 검사해야 한다면?')

<br/>

### 도커 이미지 크기를 줄이는 방법

---

* 가벼운 베이스 이미지를 사용한다.
* Dockerfile 명령을 체인으로 사용한다. (레이어를 줄이는 절차 / 자주 바뀌는 것은 레이어를 적절히 분배) - 레이어는 run 의 개수와 맞먹게 생긴다.
* 빌드 도구를 설치하지 않는다. (ex, spring boot - jdk)
* 패키지 관리자를 정리한다.

<br/>

### 도커 컨테이너 평균 지속시간 2.5일

---

<br/>

### 도커 컨테이너

---

* 이미지를 실행한 상태 - 읽기/쓰기가 가능한 파일 시스템
* 실행된 독립 애플리케이션. **컨테이너는 가상 서버가 아니다**
* 

<br/>

### 





#### 용어

카산드라 / Rebbit MQ / immutable infrastructure / copy on write / nGinex / provisioning (프로비져닝) / cowboy (linux utility) / jdk, jre / 하시코프

