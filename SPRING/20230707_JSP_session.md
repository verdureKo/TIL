# 세션 이해

[세션을 사용한 로그인 처리]
서버 세션을 사용하면 클라이언트의 상태를 저장할 수 있습니다.
쿠키와의 차이점은 세션은 웹 브라우저가 아니라 서버에 값을 저장한다는 점입니다.
서버는 세션을 사용해서 클라이언트 상태를 유지할 수 있기 때문에,
로그인한 사용자 정보를 유지하기 위한 목적으로 세션을 사용합니다.

1. 세션 사용하기 : session 기본 객제
웹 브라우저에 정보를 보관할 때 쿠키를 사용한다면,
세션은 웹 컨테이너에 정보를 보관할 때 사용합니다.
세션은 오직 서버에만 생성됩니다.

["그림_2) 세션 동작 방식" 참고]

세션은 웹 브라우저와 연관된 서버 영역 저장 공간입니다.
웹 컨테이너는 기본적으로 한 개의 웹 브라우저마다 한 개의 세션을 생성합니다.
예를 들어, JSP1과 JSP2가 세션을 사용한다고 가정해 봅니다.
이 경우 웹 브라우저1이 JSP1과 JSP2를 실행하면, 웹 브라우저1과
관련된 세션1을 사용합니다. 웹 브라우저2가 JSP1과 JSP2를
실행하면 웹 브라우저2와 관련된 세션2를 사용합니다.
즉, 같은 JSP 페이지라도 웹 브라우저에 따라 서로 다른 세션을 사용합니다.

웹 브라우저마다 세션이 따로 존재하기 때문에,
세션은 웹 브라우저와 관련된 정보를 저장하기에 알맞은 장소입니다.
즉, 쿠키가 클라이언트 측의 데이터 보관소라면 세션은 서버 측의 데이터 보관소인 것입니다.
쿠키와 마찬가지로 세션도 생성을 해야만 정보를 저장할 수 있습니다.
일단 세션을 생성하면 session 기본 객체를 통해서 세션을 사용할 수 있습니다.

1) 세션 생성하기
JSP에서 세션을 생성하려면 다음과 같이 page 디렉티브의 session 속성을 "true"로 지정하면 됩니다.
[다음]
<%@ page contentType = ... %>
<%@ page session = "true" %>
<%
   ...
   session.setAttribute("userInfo", userinfo);
   ...
%>

그런데 page 디렉티브의 session 속성은 기본값이 true이므로 session 속성값을 false로
지정하지만 않으면 세션이 생성됩니다. 세션이 생성되면 session 기본 객체를 통해서
세션을 사용할 수 있습니다.

"그림_2) 세션 동작 방식"과 같이 세션을 사용하는 서버 프로그램에
웹 브라우저가 처음 접속할 때 세션을 생성하고, 이후로는 이미 생성된 세션을 사용합니다.

2) session 기본 객체
세션을 사용한다는 것은 session 기본 객체를 사용한다는 것을 말합니다.
session 기본 객체는 request 기본 객체와 마찬가지로 속성을 제공하므로
setAttribute(), getAttribute() 등의 메서드를 사용하여
속성값을 저장하거나 읽어올 수 있습니다. 추가로 세션은 세션만의 고유 정보를 제공하며,
이들 정보를 구할 때 사용하는 메서드는 다음과 같습니다.
[다음 : session 기본 객체가 제공하는 세션 정보 관련 메서드]
메서드			리턴 타입		의미
getld()			String	세션의 고유 ID를 구합니다(세션 ID라고 합니다)
getCreationTime()		long	세션이 생성된 시간을 구합니다.
                                    	시간은 1970년 1월 1일 이후 흘러간 시간을 의미하며,
                                    	단위는 1/1000초입니다.
getLastAccessedTime()	long	웹 브라우저가 가장 마지막에 세션에 접근한 시간을 구합니다.
                                                시간은 1970년 1월 1일 이후 흘러간 시간을 의미하며,
                                                단위는 1/1000초입니다.
앞서 웹 브라우저마다 별도의 세션을 갖는다고 했습니다. 이때 각 세션을 구분하기 위해
세션마다 고유 ID를 할당하는데 그 아이디를 세션 ID라고 합니다. 웹 서버는 웹 브라우저에
세션 ID를 전송합니다. 웹 브라우저는 웹 서버에 연결할 때마다 매번 세션 ID를 보내서
웹 서버가 어떤 세션을 사용할지 판단할 수 있게 합니다.

웹 서버는 세션 ID를 이용해서 웹 브라우저를 위한 세션을 찾기 때문에,
웹 서버와 웹 브라우저는 세션 ID를 공유할 수 있는 방법이 필요합니다.
세션 ID를 공유하기 위해 사용하는 것이 쿠키입니다.
쿠키 목록 중에 이름이 JSESSIONID인 쿠키가 있는데,
이 JSESSIONID 쿠키가 세션 ID를 공유할 때 사용하는쿠키입니다.

* JSP 소스 코딩 : 메서드를 사용하여 현재 사용 중인 세션 정보를 보여주는 JSP 소스 코딩
[source08 폴더 안에 sessionInfo.jsp 소스 코딩]

* 기존 세션 정보가 없다면,
① makeCookie.jsp로 쿠키 생성해줌
② viewCookies.jsp로 쿠키 생성 확인함
③ sessionInfo.jsp로 세션 정보 확인함

3) 기본 객체의 속성 사용
한 번 생성된 세션은 지정한 유효 시간 동안 유지됩니다. 따라서, 웹 어플리케이션을
실행하는 동안 지속적으로 사용해야 하는 데이터의 저장소로 세션이 적당합니다.
request 기본 객체가 하나의 요청을 처리하는 데 사용되는 JSP 페이지 사이에서
공유된다면, session 기본 객체는 웹 브라우저의 여러 요청을 처리하는
JSP 페이지 사이에서 공유됩니다. 따라서, 로그인한 회원 정보 등 웹 브라우저와
일대일로 관련된 값을 저장할 때에는 쿠키 대신 세션을 사용할 수 있습니다.

세션에 값을 저장할 때는 속성을 사용합니다. 속성에 값을 저장하려면
setAttribute() 메서드를 사용하고, 속성값을 읽으려면 getAttribute() 메서드를 사용합니다.

* JSP 소스 코딩 : 사용자 정보 중의 하나인 회원 아이디와 이름을 저장하는 JSP 소스 코딩
[source08 폴더 안에 setMemberlnfo.jsp 소스 코딩]

setMemberlnfo.jsp를 실행하면 session 기본 객체에 저장한 두 속성을 사용할 수 있게 됩니다.

[쿠키 vs 세션 : 참고 사항]
쿠키 대신에 세션을 사용하는 가장 큰 이유는 세션이 쿠키보다 보안에서 앞선다는 점입니다.
쿠키의 이름이나 데이터는 네트워크를 통해 전달되기 때문에 HTTP 프로토콜을 사용하는 경우
중간에 누군가 쿠키의 값을 읽어올 수 있습니다. 하지만, 세션의 값은 오직 서버에만
저장되기 때문에 중요한 데이터를 저장하기에 알맞은 장소입니다.
세션을 사용하는 두 번째 이유는 (흔치 않지만) 웹 브라우저가 쿠키를 지원하지 않을 경우 또는
강제적으로 쿠키를 막는 경우 쿠키는 사용할 수 없게 되지만,
세션은 쿠키 설정 여부에 상관없이 사용 할 수 있다는 점입니다.
서블릿/JSP는 쿠키를 사용할 수 없는 경우, URL 재작성 방식을 사용해서 세션 ID를
웹 브라우저와 웹 서버가 공유할 수 있습니다. 하지만. 세션은 여러 서버에서 공유할 수 없습니다.
예를 들어. www.daum.net의 세션과 mail.daum.net의 세션은 다릅니다.
반면에 쿠키는 도메인을 이용해서 쿠키를 여러 도메인 주소에 공유할 수 있습니다.
이런 이유로 Daum과 같은 포털 사이트는 쿠키를 이용해서 로그인 정보를 저장합니다.

4) 세션 종료
세션을 유지할 필요가 없으면 session. invalidate() 메서드를 사용해서 세션을 종료합니다.
세션을 종료하면 현재 사용 중인 session 기본 객체를 삭제하고 session 기본 객체에
저장했던 속성 목록도 함께 삭제합니다.

* JSP 소스 코딩 : 세션을 종료하는 JSP 소스 코딩
[source08 폴더 안에 closeSession.jsp]
세션을 종료하면 기존 session 객체를 제거하고, 세션 종료 후
다음 요청에서 session을 사용하면 새로운 session 기본 객체를 생성합니다.

① http://localhost:8080/source08/sessionInfo.jsp 실행
② http://localhost:8080/source08/closeSession.jsp 실행
③ http://localhost:8080/source08/sessionInfo.jsp 실행

먼저 sessionlnfo.jsp를 실행하면 세션을 생성합니다. 기존에 이미 세션을 생성했다면
생성된 세션을 사용합니다. 이 상태에서 closeSession.jsp를 실행하면 세션을 종료하고
사용 중인 session 객체를 제거합니다. 세션을 종료한 상태에서 다시 sessioninfo.jsp를
실행하면, 세션이 존재하지 않으므로 새로운 세션을 생성합니다.

5_내용 참고) 세션 유효 시간
세션은 최근 접근 시간을 갖습니다. session 기본 객체를 사용할 때마다
세션의 최근 접근 시간은 갱신됩니다.

세션은 마지막 접근 이후 일정 시간 이내에 다시 세션에 접근하지 않는 경우
자동으로 세션을 종료하는 기능을 갖고 있습니다.

* 세션 유효 시간은 두 가지 방법으로 설정할 수 있습니다.
첫번째 방법은 WEB-INF\web.xml 파일에 다음과 같이 <session-config> 태그를
사용하여 세션 유효 시간을 지정하는 방법입니다.
[다음]
〈?xml version=”1.0” encoding="euc-kr"?>
〈web-app xmlns="http:/xmlns.jcp.org/xml/ns/javaee"
  xmlns: xsi="’http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
  http://xmlnsjcp.org/xml/ns/javaee/web-app_3_l.xsdn"
  version="3.1">

<session-config>
  <!-- 여기서는 세션 타임아웃 시간을 50분으로 지정했음 -->
   <session-timeout>50</ session-timeout>
</session-config>
</web-app>

〈session-timeout〉태그 값을 세션의 유효 시간으로 사용합니다.
이 값의 단위는 분입니다. 위 코드는 세션 타임아웃 시간을 50분으로 지정하고 있습니다.

세션의 유효 시간을 지정하는 두 번째 방법은 session 기본 객체가 제공하는
setMaxInactiveInterval() 메서드를 사용하는 것입니다

예를 들어, 세션의 유효 시간을 60분으로 지정하고 싶다면
다음과 같이 setMaxInactiveInterval() 메서드를 사용하면 됩니다.
[다음]
<%
   session.setMaxInactiveInterval(60*60);  // 60초(1분) * 60 = 60분 설정했음
%>

web. xml 파일에서 분 단위로 유효 시간을 설정했던 반면
session.setMaxInactiveInterval() 메서드는 초 단위로 유효 시간을 설정합니다.
<session-timeout>의 값을 0이나 음수로 설정하면 세션은 유효 시간을 갖지 않게 됩니다.
이 경우 명시적으로 session.invalidate() 메서드를 호출하기 전까지 세션 객체가
서버에 유지됩니다. 즉，유효 시간이 없는 상태에서 session.invalidate() 메서드를
실행하지 않으면, 세션 객체가 계속 메모리에 남게 되어 메모리 부족 현상이 발생하게 됩니다.

제거되지 않는 세션 객체로 인해 메모리가 부족해지는 현상을 방지하려면,
반드시 세션 타임아웃 시간을 지정해주어야 한다.

6_내용 참고) request.getSession()을 이용한 세션 생성
HttpSession을 생성하는 또 다른 방법은 request 기본 객체의 getSession() 메서드를
사용하는 것입니다. request.getSession() 메서드는 현재 요청과 관련된 session 객체를
리턴합니다. 다음 코드는 사용 예시 입니다.
[다음]
request.getSession()을 이용해서 세션을 구하므로,
page 디렉티브의 session 속성값은 false로 지정합니다.

〈%@ page session="false" %>
<%
   HttpSession httpSession = request.getSession(); 
   List list = (List)httpSession.getAttribute("list");
   list.add(productld);
%>

request.getSession() 메서드는 session이 존재하면 해당 session을 리턴하고
존재하지 않으면 새롭게 session을 생성해서 리턴합니다.

session이 생성된 경우에만 session 객체를 구하고 싶다면, getSession() 메서드에
false를 인자로 전달하면 됩니다. request.getSession(false)를 실행하면
세션이 존재하는 경우에만 session 객체를 리턴하고 세션이 존재하지 않으면
null을 리턴합니다.

〈%@ page session="false" %>
<%
   HttpSession httpSession = request.getSession(false);
   List list = null;
   if (httpSession != null) {
      list = (List)httpSession.getAttribute("list");
   } else (
   list = Collections.emptyList();
   }
%>

2. 세션을 사용한 로그인 상태 유지
세션을 사용해서 로그인을 처리하는 방식은 쿠키를 사용한 방식과 비슷합니다.
① 로그인에 성공하면 session 기본 객체의 특정 속성에 데이터를 기록합니다.
② 이후로 session 기본 객체의 특정 속성이 존재하면 로그인한 것으로 간주합니다.
③ 로그아웃할 경우 session.invalidate() 메서드를 호출하여 세션을 종료합니다.

1) 인증된 사용자 정보 session 기본 객체에 저장하기
세션을 사용해서 로그인 상태를 유지하려면 session 기본 객체의 속성에
로그인 성공 정보를 저장하면 됩니다.

* JSP 소스 코딩 : session 기본 객체의 특정 속성을 로그인 상태 정보로 사용하는 JSP 소스 코딩
[source08 폴더 안에 sessionLogin.jsp 소스 코딩]

sessionLogin.jsp는 id 요청 파라미터와 password 요청 파라미터가 같으면
로그인에 성공한 것으로 간주하고, session 기본 객체의 "MEMBERID” 속성에
사용자 아이디 정보를 저장합니다. 즉, "MEMBERID" 속성이 존재하면
현재 사용자는 로그인한 사용자로 간주합니다.

* JSP 소스 코딩 : sessionLogin.jsp에 아이디와 암호를 전송하는 폼을 보여주는 JSP 소스 코딩
[source08 폴더 안에 sessionLoginForm.jsp 소스 코딩]

2) 인증 여부 판단
session 기본 객체에 로그인 상태를 위한 속성의 존재 여부에 따라 로그인 상태를
판단할 수 있습니다. 

* JSP 소스 코딩 : sessionLogin.jsp은 로그인에 성공하면 MEMBERID 속성에
                     로그인 상태 정보를 보관하므로, session 기본 객체의
                     "MEMBERID" 속성을 사용해서 로그인 여부를 판단하면 됩니다.
[source08 폴더 안에 member폴더 안에 sessionLoginCheck.jsp 소스 코딩]

3) 로그아웃 처리
로그아웃을 처리할 때에는 session.invalidate() 메서드를 사용하여 세션을 종료하면 됩니다.

* JSP 소스 코딩
[source08 폴더 안에 member폴더 안에 sessionLogout.jsp 소스 코딩]

session.invalidate() 메서드를 호줄하지 않고, 다음과 같이 로그인 상태를 보관할 때
사용한 session 기본 객체를 모두 삭제해도 로그아웃한 효과를 낼 수 있습니다.
[다음]
session.removeAttribute("MEMBERID");

하지만, 로그인할 때 session 기본 객체에 추가하는 속성이 늘어나면
로그아웃 코드도 함께 변경해야 하므로,
session.invalidate() 메서드를 사용하는 것이 좋습니다.

