---
layout: post
title:  "[Spring]formal하게 스프링 시큐리티에서 제공하는 UserDetails 와 AuthenticationProvider 그대로 사용하여, 회원가입이 아닌 로그인 구현해보기"
date:   2018-09-09 
categories: Spring
comments: false
---
 spring boot starter web

 2.0.3

 spring boot starter security

 2.0.3 

 mysql connector java

 5.1.46

 mybatis spring boot starter

 1.3.2

 (maybe) sprig session

 1.0.0

  


![](https://t1.daumcdn.net/cfile/tistory/998B293C5B94925032)

  


  


  


2) Service - 'UserService' class

  


- 'UserDetailsService' 상속 받아야 되고, 밑에 주석에 설명 있다.

- DB에서 읽고, 생성하고, 삭제하는 메소드 만들어 주고,

- 'username' 사용자 ID, 혹은 뭐 사용자 구별할 수 있는 고유한 값으로 해당 사용자가 어떤 권한을 가지고 있는지 가져온다.

- passwordEncoder 메소드는 아마 사용 안할 거 같은데 일단 내비둬 본다.

  


  


  


3) ServiceImpl - 'UserServiceImpl' class  


  


- Service 클래스 구현체

- 'UserMapper' 아직 구현 안 하였고, 'SHA256Encrption' 은 만든 패스워드 암호화라서 본인 것이 있다면 본인 거 쓰던가, 'PasswordEncoder' 검색 하면 암호화 관련 클래스 나오니까 검색해서 찾아보도록.

- 'UserDetailsService' 클래스 상속 받으면 'loadUserByUsername' 메소드 구현 해야된다. 저 클래스 까보면 있다.

- 'PasswordEncoder' 상속 받으면 메소드 2개 구현 해야되는데 엄청 쉬움 좀 있다가 나옴.

- 'getAuthorities' 라는 매소드가 나오는데 리턴 타입이 심상치가 않다. 'GrantedAuthority'는 이제 또 Security에서 쓰이는 리턴 타입인데 이걸 'mybatis'에서 지원하는 기본적인 뭔가 포멀한 리턴 값이 아니잖아, String, int, 이런 것 처럼 그래서 저거를 또 처리해 주는 'TypeHandler' 라는 놈을 구현해야되는데 그렇게 어렵지 않음.

- 'readUser' 메소드 잘 보면 set 메소드로 객체에 값을 지정해 주는데 저건 이제 또 DB에 '권한(Authority)' 라는 컬럼 두개 인가 세개인가 짜리 만들거여, 거기에서 'username' 에 대한 권한을 뽑아서 DTO 객체 완성 시키는 거여.

- 'createUser' 메소드도 잘 보면 여기서 암호화 해서 이제 DB에 저장하는 거여. 그리고, 'User' 도 저장하지만 '권한(Authority)' 도 저장한다. DB에 테이블 두개 만드렁.

- 나머진 soso 하니까 넘어가자.

  


  


  


4) Util class - 'SHA256Encryption' implements 'PasswordEncoder' class

  


- 이거는 사실 내가 만든 클래스는 아니고 어디서 줏어 온건데 다양한 암호화 방식 중에 'SHA-256'을 모태로 하는 거.

- 뭐 BEncrypt 인가 뭔가랑 다른거 많이 있는데 나는 그냥 있어서 이걸로 했고, 다른거 써도 됨. 단, 지금 진행하는 예제에서는 꼭 'PasswordEncoder'를 상속 받는 class를 구현해야 함.

- 'encrypt' 메소드는 이제 파라미터로 패스워드가 들어오면 암호화해주는 거. 왜 static으로 했는지는 나도 모른다.

- 저 상속 받은 클래스 구현하면, 드디어, 세번째 말하는, 구현해야 하는 2가지 매소드를 구현 할 것이다. 'encode' 라는 놈이랑, 'matches' 라는 놈인데 딱 봐도 직관적이여, 'encode'는 암호화 하는 놈, 'matches'는 입력 받은 비밀번호랑 DB에 저장되어 있는 놈이랑 같은 지 확인 하는 놈.

 

  


  


5) Util class - 'AuthorityTypeHandler' implements 'BaseTypeHandler<SimpleGrantedAuthority>' class

  


- 이거슨, 그 우리가 이제 ORM을 'myBatis'로 쓰면서 DB로 쿼리문을 날리고, DB에서 리턴 받는 그런 일련의 과정을 거치는데, DB에도 아래 같은 'DataType'을 정해주잖아, 저걸로 이제 DB에 저장도 되고 꺼내 올때도 저 형식으로 꺼내오기도 하는데 이제 꺼내 올때 우리가 'mapper' 에서 부터 아예 'resultType' 자체를 'GrantedAuthority' 로 받고 싶다는 거지, 근데 그게 없잖아? 그래서 그런 특별한, 아주 유니크한 타입을 지원하기 위한 것이 저 Base 뭐시기를 상속 받아서 구현하는 거야.

  


![](https://t1.daumcdn.net/cfile/tistory/99265A445B94A95A02)

- 주석 설명 참고.  


  


  


  


6-1) 'Mapper' class - 'UserMapper' class

  


- 걍 매퍼 클래스

- 근데 저기 주석 처리 된 메소드는 내가 맨 상단에 링크 걸어 놓은 아주 친절한 분의 블로그에서 처음에는 '권한'을 그냥 String으로 처리했다가 바꾼 걸 따라 한 것을, 남겨둔 것.

- 주석이 친절하다. 이래서 주석을 잘 달아놓으라는 것 같다.

  


  


  


6-2) 'Mapper' xml - 'UserMapper' xml

  


- 일반적인 mapper 인거 같은데 'readAuthority' 와 'createAuthority' 만 보고 넘어가자.

- 위에서 말했던 것 처럼 'readAuthority' 에서 'resultType'을 아주 패키지명까지 싸잡아다가 넣어 버렸다. 음 끝.

- 'createAuthority' 이놈은 service 클래스에서 잘 안보여서 당황했을 수도 있겠지만, 'createUser'에서 'Authority' 테이블도 채워줘야 하기 때문에 만들었고, 기본적으로 이 예제에서는 유저가 여러 권한을 갖을 수 있다고 생각한다. 예를들어, 어떤 사용자가 '관리자' 이면서 '회원' 이면서 '임원' 인 이런 좀 뭐랄까 다중 감투 시스템이다.

- 그래서 '권한' 테이블에 여러 감투가 들어가야 하니까 foreach' 구문이 사용 되었고 나는 저 문법이 어색해서 봐둘 필요가 있고.

  


  


  


6-3) XML Mapper 설정

  


- 혹시 몰라서 올려둔다.

- 패키지명, aliase 랑 리소스 파일 path.

  


  


  


7) Configure class - 'SecurityConfigure' implements 'WebSecurityConfigureAdaptor' class  


  


- 대망의 마지막인데 내가 짜놓은 코드를 갈아 엎어서, 보고 배운 블로그 코드를 인용한다.

- 아마 이 밑에 있는 클래스로 돌리면 에러가 날 것이다.

- 설정에 대한 다양한 메소드가 있는데 필요한 기능을 찾아보면 될 것이고, 그 필요한 기능이 뭐가 있는지 내가 알고 있는 선에서만 언급하고 넘어가겠다.

- 특정 리소스 파일들은 검사하지 않는 메소드가 있다. -> 'configure(WebSecurity web)'

- 더 있는데 배움의 한계가 여기 까지인 듯 하다..

- 필수적으로 'configure(HttpSecurity http)' 메소드를 구현 하면 되는데, '.and()' 를 사용해서 Security에서 제공하는 로그인 폼을 사용할지, 로그인 폼 path를 따로 줄지 결정 할 수 있고, 권한 마다 접근 가능한 페이지 설정, 로그아웃 설정, 로그아웃도 로그아웃 되는 페이지 설정 가능하는 등 여러가지 설정을 줄 수 있다. 본인의 프로젝트에 맞게 view 를 구성하여 사용하길 바란다.

  


  


