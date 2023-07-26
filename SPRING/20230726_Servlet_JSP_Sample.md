# MVC패턴 회원가입 로그인 암호변경 예제

## 회원가입을 위해 구현할 코드

![Alt text](/assets/image.png)
1. 회원 가입 기능은 다음과 같은 기능을 제공해 줍니다.
1) 입력 폼에 아이디, 이름, 암호, 암호 확인을 입력하고 전송하면 가입에 성공합니다.
2) 동일한 아이디를 가진 회원이 존재하면 에러 메시지와 함께 다시 폼을 보여줍니다.
3) 입력한 암호와 암호 확인이 일치하지 않으면 에러 메시지와 함께 다시 폼을 보여줍니다.
2. 위의 회원 가입 기능 구현에 연관된 클래스의 구성은 다음과 같습니다.
1) JoinHandler : 사용자의 요청을 받는다. 사용자가 폼을 요청한 경우 폼을 보여줍니다.
폼 데이터를 전송한 경우 JoinService를 이용해서 회원 가입을 처리합니다.
- joinForm.jsp : 회원 가입 폼을 보여 줍니다.
- joinSuccess.jsp : 회원 가입 처리에 성공한 경우 결과를 보여줍니다.
2) JoinService : 회원 가입 기능을 구현합니다.
- JoinRequest : 회원 가입할 때 필요한 데이터를 담게 됩니다.
폼에 입력한 값을 이 객체에 담아서 JoinService에 전달합니다.
3) MemberDao : member 테이블과 관련된 쿼리를 실행합니다.
4) Member : member 테이블과 관련된 클래스로서 회원 데이터를 담게 됩니다. VO 역할을 합니다.

## 로그인 기능을 위해 구현할 코드

![Alt text](/assets/image-1.png)
1. 로그인은 인증(authentication)의 한 방법입니다. 서비스를 사용하는 사람이 본인이 맞는지 확인하는
것을 인증이라고 합니다. 로그인 상태를 유지한다는 것은 인증 상태를 유지한다는 것을 의미하며, 
웹 어플리케이션에서 보통 이런 인증 상태 정보는 서버 세션이나 쿠키에 저장합니다.
2. 로그인 기능은 다음과 같은 기능을 제공합니다.
1) 로그인 요청을 하면 로그인을 위한 폼을 보여줍니다.
2) 입력 폼에 아이디와 암호를 입력하고 전송하면 검사합니다.
3) 아이디나 암호가 맞지 않으면 에러 메시지와 함께 다시 폼을 보여줍니다.
4) 아이디와 암호가 일치하면 첫 화면으로 이동합니다.
3. 구현 코드는 다음과 같습니다.
1) LoginHandler : 사용자의 요청을 받습니다. 사용자가 폼을 요청한 경우 폼을 보여주고,
폼 데이터를 전송한 경우 LoginService를 이용해서 인증을 처리합니다.
2) loginForm.jsp : 로그인폼을 보여줍니다.
3) index.jsp : board 웹 어플리케이션의 첫 화면을 보여줍니다.
4) LoginService : 인증 관련 기능을 구현합니다.
5) User : 인증에 성공한 사용자의 정보를 담게 됩니다. 이 객체를 세션에 저장합니다.

## 암호 변경을 위해 구현할 코드

![Alt text](/assets/image-2.png)
1. 암호 변경 기능은 로그인한 경우에만 실행할 수 있으므로, 로그인 여부 검사를 적용하기에 좋습니다.
2. 구현 코드는 다음과 같습니다.
1) Member : 암호가 일치하는지 확인하고 암호를 변경하는 기능을 제공합니다.
2) MemberDao : member 테이블의 데이터를 수정하는 기능을 제공합니다.
3) ChangePasswordService : 특정 사용자의 암호를 변경하는 기능을 제공합니다.
사용자 아이디, 현재 암호, 신규 암호를 입력으로 받아서 암호를 변경 처리 합니다.
4) ChangePasswordHandler : 웹 브라우저의 암호 변경 요청을 처리합니다.
GET요청이면 changePwdForm.jsp를 이용해서 폼을 보여줍니다.
POST 요청이면 ChangePasswordService를 이용해서 암호 변경 기능을
실행 합니다. 암호 변경에 성공하면 changePwdSuccess.jsp를 View(뷰)로 사용합니다.

select host, user from user;
    -- '%'는 외부권한을 허용한다는 정의이며, root로 외부권한을 허용하는 건 위험할 수 있습니다.
    -- 이에, 개발 후 아래와 같이 root 권한을 회수 처리 바랍니다.
    revoke all on *.* from root@'%';
    flush privileges;
    drop user root@'%';
    select host, user from user;

======================================================================

  3) MySQL 워크벤치 : board.member 테이블 생성 쿼리

	use board;

	create table board.member (
	    memberid varchar(50) primary key,
	    name varchar(50) not null,
	    password varchar(10) not null,
	    regdate datetime not null
	) engine=InnoDB default character set = utf8;

	select * from board.member;


7. 기능 확인

  1) BOARD_SIGNUP 프로젝트 클릭 선택 - 마우스 우클릭 - Run As - Run On Server
     (index.jsp 파일 클릭 - 마우스 우클릭 - Run As - Run On Server 해도 됨)
     (index_custum_tag_version.jsp 파일 클릭 - 마우스 우클릭
      - Run As - Run On Server 해도 됨. 이때, CT는 커스텀 태그 활용 나타냄)

  2) [회원가입하기] 클릭 - 아이디: 란에 예시(jangnara) 입력
      - 이름: 란에 예시(장나라) 입력
      - 암호: 란에 예시(12345) 입력
      - 확인: 란에 예시(12345) 입력
      - 가입신청 버튼 클릭
      - "장나라님, 회원 가입에 성공했습니다." 메시지 확인

  3) http://localhost:9001/login.do 로 이동해서
     - 아이디: 란에 예시(jangnara) 입력
     - 암호: 란에 12345 입력
     - 로그인 버튼 클릭

  4) [암호변경] 클릭 - 현재 암호: 란에 예시(12345) 입력
      - 새 암호: 란에 예시(54321) 입력 - 암호 변경 버튼 클릭
      - "암호를 변경했습니다." 메시지 확인

  5) http://localhost:9001/login.do 로 이동해서
     - 아이디: 란에 예시(jangnara) 입력
     - 암호: 란에 12345 입력
     - 로그인 버튼 클릭
     - "아이디와 암호가 일치하지 않습니다." 메시지 확인
     - 암호: 란에 변경된 암호 예시(54321) 입력 후 로그인 버튼 클릭 - 로그인 확인

  6) [로그아웃하기] 버튼 클릭 - http://localhost:9001/index.jsp로 이동되는거 확인
      
  7) MySQL 워크벤치에서 다음의 쿼리문으로 데이터베이스 회원 정보 확인
 
    select * from board.member;

### 응답값 메모

* 톰캣 9.0 HttpServletResponse 응답 코드 전송 상수값 정의

https://tomcat.apache.org/tomcat-9.0-doc/servletapi/javax/servlet/http/HttpServletResponse.html

* 톰캣 8.5 HttpServletResponse 응답 코드 전송 상수값 정의

https://tomcat.apache.org/tomcat-8.5-doc/servletapi/javax/servlet/http/HttpServletResponse.html

static int	SC_NOT_FOUND
          404 응답 코드 전송(요청한 자원이 존재하지 않음)
          요청 된 리소스를 사용할 수 없음을 나타내는 상태 코드 (404)입니다.

static int	SC_INTERNAL_SERVER_ERROR
          HTTP 서버 내부 오류로 인해 요청을 수행하지 못함을 나타내는 상태 코드 (500)입니다.

static int	SC_METHOD_NOT_ALLOWED
          405 응답 코드 전송 (허용되지 않는 메소드 응답)
          지정된 메서드가 식별 된 리소스에 대해 허용되지 않음을 나타내는 상태 코드 (405) 입니다.

static int	SC_FORBIDDEN
          403 응답 전송(서버 응답 실행 거부)
          서버가 요청을 이해했지만 수행을 거부했음을 나타내는 상태 코드 (403)입니다.