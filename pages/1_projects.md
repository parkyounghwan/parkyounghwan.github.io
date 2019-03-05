---
layout: page
title: Projects
comments: true
permalink: /projects/
---

* content
{:toc}

# All my projects
Following are projects started by me. 

## Carrier
> DB 내의 대용량 데이터 CSV 다운로드 시스템  

* 기간: 2018-02 ~ 2018-05
* 프로젝트 개요  
데이터 베이스에 저장되어 있는 약 2천만건의 데이터를 많은 사용자들이 정확하게 다운로드 받아 볼 수 있는 시스템
* 사용 기술: Java, Spring boot, MySQL, myBatis, Microsoft Azure.
* 내용
~~~
이 시스템은 크게 두개의 프로젝트로 나누어 집니다. 작업을 수행하는 워커 인스턴스와 이 인스턴스들에게 작업을 분배하는 서버가 있습니다. 이들은 각각 'Interceptor(인터셉터)' 와 'Carrier(캐리어)' 라 칭합니다. 그리고 이들은 서로 REST API 로 통신 합니다.  

인터셉터는 작업 요청을 받으면, 요청으로 받은 시간대의 데이터들을 CSV로 변환하여 Azure에 BLOB Storage에 저장시켜 줍니다. WAS의 부하를 줄이기 위해 정적 리소스를 따로 분리하였습니다. 그리고 분리된 정적 리소스를 효율적으로 관리하기 위해 BLOB Storage를 선택하게 되었습니다.  데이터를 MySQL 에서 불러 올 때는, 부하를 줄이기 위해 페이징으로 나눠서 데이터를 가져오고 이어쓰는 방식으로 개발 했습니다. Azure의 blob은 이어쓰기를 지원하지 않아 로컬에 임시 파일을 만들어 이어 쓴 후, Azure로 업로드 시키고, 임시 파일을 삭제하는 방식으로 구현했습니다.  

캐리어는 전역 동기화 큐를 이용하여, 변환 요청이 올 때마다 큐에 작업을 등록합니다. 또한 캐리어에는 인터셉터의 수만큼 스레드가 돌고 있습니다. 하나의 스레드 당 하나의 인터셉터에 매칭 됩니다. 큐에 작업이 등록 되면, 놀고 있는 스레드에서 작업을 가져와서 인터셉터에 할당 합니다. 요청과 작업은 비동기적이며, 사용자는 작업이 끝날 때 까지 Response를 기다리지 않아도 됩니다. 작업이 등록되었다는 알림은 받게 됩니다. 또한 작업이 완료되면 CSV 파일이 저장 된 BLOB 저장소 주소를 조회 할 수 있으며, 이 주소를 통해 CSV 파일을 다운로드 받을 수 있습니다.  

이러한 설계를 통해 요청수가 많아 지더라도, 인터셉터의 인스턴스를 늘리면 됨으로 빠른 처리가 가능하게 됩니다. 또한 사용자의 체감 속도에서도 큰 개선이 이루어 질 수 있었습니다.
~~~

* GitHub Repository  
   * [github.com/parkyounghwan/Carrier](https://github.com/parkyounghwan/Carrier)  
   * [github.com/parkyounghwan/Interceptor](https://github.com/parkyounghwan/Interceptor)

## markdown sample
* Started: 2004-present
* Website: [www.nplproject.com](http://www.nplproject.com)
   * NPL Code Wiki
   * NPL language service and debugger

NPL(Neural Parallel Language) is a new programming language. It was started as my exploration of coding logics in a networked environment.    
Throughout the years, I have written over a million lines of code with it. All my other projects since 2005 is written in it. 
