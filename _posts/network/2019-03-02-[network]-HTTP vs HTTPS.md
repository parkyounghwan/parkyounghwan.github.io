---
layout: post
comments: false
categories: Network
---

> HTTP 와 HTTPS 의 차이를 알아보고 나아가, HTTP/1.x 와 HTTP/2.0 에 대해서 알아본다.  

우선, HTTP는 웹 브라우져(Client) 와 웹 서버(Server) 간의 데이터를 주고 받기 위한 약속(protocol) 이다. 데이터는 HTML 같은 문서를 요청하고 서버에서는 데이터를 Text 형태로 보낸다. 따라서 네트워크 안에서 신호를 가로채게 된다면 내용을 그대로 볼 수 있다. `HTTPS`는 주고 받는 종단간에 __암호화__ 하여 연결한다. 

![public-key-secure](/static/img/public-key-secure.jpg)  
### 공개키 암호화 방식
---  
'암호화', '복호화' 할 수 있는 서로 다른 키 2개(A, B)가 있다. 이 두개의 키는 서로 'A' 키로 암호화 하면 반드시 'B' 키로만 복호화 할 수 있고, 'B' 키로 암호화 하면 반드시 'A' 키로만 복호화 할 수 있다.
  
![Multiplaxing](/static/img/Multiplaxing.png){: .center}

# +
---
* TLS/SSL
    * Transport Layer Security / Secure Socket Layer
    * 인터넷과 같이 TCP/IP 네트워크를 사용하는 통신에 적용.
    * 통신 과정에서 전송 계층 종단간 보안과 데이터 무결성을 확보.  
  
* TCP/IP 와 HTTP
    * TCP/IP 프로토콜은 HTTP 와 맞물려 동작한다.
    * 둘은 동작하는 계층이 다르다. (TCP/IP, Transport 계층 / HTTP, Application 계층)
    * HTTP, HTTPS, FTP 등의 프로토콜은 TCP/IP 위에서 동작하는 것.
    * HTTP 는 TCP/IP 위에서 어떤 형태로 웹에서 작동할지를 정해놓은 통신 프로토콜. (하이퍼텍스트를 전송하는 규약)
    * HTTP 통신은 비동기 통신을 기본으로 하여, 연결성이 없다. (Stateless, 전송 방식에 따른 패러다임이 버전에 따라서 달라진다, HTTP1.0 vs HTTP1.1 vs HTTP2.0 커넥션 관리하는 방식이 다르다.)
    * 데이터의 형태가 다르다. (TCP -> binary, HTTP -> String)
    * 연결 방식, TCP 는 언제나 서버와 연결돼있어야한다, Request 없이도 Response 가 일어난다. HTTP 는 'keep-alive' 로 지속적인 연결은 가능하지만, 기본적으로는 close 돼 있으며, Request가 있어야 Response 가 일어난다. (TCP 의 지속적인 연결에 반대는, UDP)
  
---
#### 참고 사이트
HTTP/1.x 의 커넥션 관리 : [https://developer.mozilla.org/](https://developer.mozilla.org/ko/docs/Web/HTTP/Connection_management_in_HTTP_1.x)  
Multiplaxing - SPDY : [https://nuli.navercorp.com/](https://nuli.navercorp.com/sharing/blog/post/1132452)  
