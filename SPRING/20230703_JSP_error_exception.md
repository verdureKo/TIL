# JSP 에러 처리

1. 익셉션 직접 저리하기
모든 것이 완벽할 수는 없습니다. 개발자가 만든 코드에 문제가 발생할 수 있고
데이터베이스에 문제가 생겨서 프로그램이 올바르게 동작하지 않을 수도 있습니다.
JSP 프로그램도 실행 도중에 문제가 발생할 수 있습니다.

* JSP 소스 코딩 확인
source05 폴더 생성 - readParameterNoErrorPage.jsp 소스 코딩

앞서 readParameterNoErrorPage.jsp 소스 06행에서
 "name" 파라미터의 값을 읽어와 대문자로 변환해서 출력합니다.
만약 "name" 파라미터가 없으면 request.getPammeter("name").toUpperCase() 처리시
null을 리턴하므로 이 코드는 실행 도중에 문제가 생겨 NullPointerExoeption을 발생시킵니다.
즉, name 파라미터 없이 http://localhost:8080/chap06/readParameterNoErrorPage.jsp를 실행해보면
HTTP Status 500 에러 화면이 출력됩니다.

개발 과정에서는 에러 화면에 표시된 에러 내용을 보고 어떤 에러가 발생했는지 알 수
있어서 에러 화면을 보는 것이 도움이 됩니다. 하지만, 사용자에게 서비스를 제공하고 있는데
HTTP Status 500 에러 화면이 출력되어 사용자에게 제공하는 것은 좋아 보이지 않습니다.
아울러, 코드의 일부가 노출되기 때문에 보안 측면에서도 좋지 않습니다.
앞서 HTTP Status 500 에러 화면은 톰켓이 생성한 것입니다. 이런 에러 화면을 노출하고 싶지 않다면
try-catch문을 이용해서 익셉션이 발생할 때 알맞은 응답을 생성할 수 있습니다.

* JSP 소스 코딩 확인
source05 폴더 생성 - readParameterWithTry.jsp 소스 코딩

readParameterWithTry.jsp 소스에서 07〜11행의 try-catch 블록을
실행하는 도중에 08행의 코드에서 익셉션이 발생하면
10행의 메시지를 출력합니다. name 파라미터가 null이어서
NullPointerException이 발생하면, 에러 화면 대신에 catch 블록에서
출력한 응답이 표시됩니다. 

2. 에러 페이지 지정하기
JSP는 실행 도중 익셉션이 발생할 때 에러 화면 대신
지정한 JSP 페이지를 보여줄 수 있는 기능을 제공하고 있습니다.
익셉션이 발생하면 보여줄 JSP 페이지는 page 디렉티브의 errorPage 속성을 사용해서 지정합니다.

* JSP 소스 코딩 확인
source05 폴더 생성 - readParameter.jsp 소스 코딩

readParameter.jsp의 02행을 보면 page 디렉티브의 errorPage 속성을 지정했습니다.
name 파라미터가 존재하지 않아 07행에서 NullPointerException이 발생하면,
WAS는 자체적으로 에러 페이지를 생성하는 대신 errorPage 속성에 지정한 JSP를 실행해서
에러 화면을 생성합니다.

3. 에러 페이지 작성하기
page 디렉터브의 errorPage 속성을 사용해서 에러 페이지를 지정하면,
에러가 발생할때 지정한 에러 페이지를 사용하게 됩니다.
에러 페이지에 해당하는 JSP 페이지는 page디렉터브의 isErrorPage 속성의 값을
"true"로 지정해야 합니다.

* JSP 소스 코딩 확인
source05 폴더 생성 - viewErrorMessage.jsp 소스 코딩

page 디렉터브의 isErrorPage 속성값을 "true"로 지정하면,
JSP 페이지는 에러 페이지가 됩니다.
에러 페이지로 지정된 JSP는 exception 기본 객체를 사용할 수 있습니다.
exception 기본 객체는 JSP 실행 과정에서 발생한 익셉션 객체에 해당합니다.
즉, readParameter.jsp는 errorPage로 viewErrorMessage.jsp를 지정했는데,
readParameter. jsp를 실행하는 과정에서 NullPointerException이 발생하면,
익셉션 객체가 viewErrorMessage.jsp의 exception 기본 객체가 됩니다.

익셉션이 발생했을 때 실제로 에러 페이지가 출력되는지 확인해 봅니다.
웹 브라우저에 http://localhost:8080/source05/readParameter.jsp 입력하면
name 파라미터가 없으므로 readParameter.jsp를 실행하는 과정에서
NulIPointerException이 발생하는데,
여러 페이지로 viewErrorMessage.jsp를 지정했으므로
viewErrorMessage.jsp의 실행 결과가 출력됩니다.

인터넷 익스플로러의 경우(iexplore.exe 실행 확인), 자체적으로 제공하는
HTTP 오류 메시지가 화면에 출력됩니다.
즉, 인터넷 익스플로러에서는 다음의 경우, 에러 페이지의 응답 길이가 짧으면
에러 페이지가 출력한 내용 대신 자체 에러 화면을 표시합니다.
[다음]
① 응답의 상태 코드가 400, 404나 500 등 에러 코드이고,
② 전체 응답 결과 데이터의 길이가 주석문 포함 512바이트보다 작을 때

따라서，인터넷 익스플로러에서도 에러 페이지의 내용이 올바르게 출력되길 원한다면,
에러 페이지가 생성하는 응답 데이터가 512바이트보다 커야 합니다.
 작성하는 에러 페이지의 응답 크기가 512바이트보다 작다면,
다음과 같이 HTML 주석을 포함해서 응답 데이터의 크기가 512바이트를 넘도록 해주면 됩닏.

[다음]
〈%@ page contentType = "text/html; charset=euc-kr" %>
〈%@ page isErrorPage = "true" %>
〈!--
만약 에러 페이지의 길이가 512바이트보다 작다면，
인터넷 익스들로러는 이 페이지가 출력하는 에러 페이지를 출력하지 않고
자체적으로 제공하는 'HTTP 오류 메시지' 화면을 출력한다.
인터넷 익스플로러에서도 에러 페이지 내용을 올바르게 출력하려면
응답 결과에 이 주석과 같은 내용을 포함해서
에러 데이터가 512바이트를 넘도록 해야 합니다.
-->
위와 같은 HTML 주석을 viewErrorMessage.jsp에 포함해서 다시 실행해봅니다.
그러면, 인터넷 익스플로러에서도 에러 페이지가 생성한 결과 화면이 원하는 대로
출력되는 것을 확인할 수 있습니다.

* JSP 소스 추가 코딩 확인
source05 폴더 - viewErrorMessage.jsp 소스에 위에 [다음] 주석 내용 추가 코딩
- 인터넷익스플로러에서 예외 처리 메시지 확인함.

4. 응답 상태 코드별로 에러 페이지 지정하기
웹 서버는 존재하지 않는 페이지에 대한 요청을 받으면  404 에러 코드로 응답합니다.
참고로, 에러 코드 화면은 웹서버나 WAS 마다 다릅니다.

실제 서비스를 제공할 땐 에러 화면을 사용자에게 그대로 보여주지 않고,
알맞은 에러 페이지를 보여주는게 좋습니다.
그러기 위해서는 JSP/서블릿은 에러 코드별로 사용할 에러 페이지를
web.xml 파일에 지정할 수 있습니다.
에러 코드에 대해 보여줄 에러 페이지를 지정하려면
web.xml 파일에 다음과 같은 설정을 추가해주면 됩니다.
[다음]
<?xml version="1.0" encoding="utf-8"?>
〈web-app ...>
...
<error-page>
   <error-code> 에 러 코드〈/error-code〉
   〈location〉에러페이지의 URI</location>
</error-page>
...
〈/web-app〉

<error-page> 태그는 한 개의 에러 페이지를 지정합니다.
〈error-oode〉태그는 에러 상태 코드를 지정하고 <location>태그는
에러 페이지로 사용할 JSP 파일의 경로를 지정합니다.
예를 들어, 페이지가 존재하지 않을 때 발생하는 404 코드와 서버 내부 에러
코드인 500 에러 코드에 대해서 에러 페이지로 각각 /error/error404.jsp와
/error/error500.jsp를 사용하고 싶다면 web.xml 파일에 〈error-page>태그를 추가하면 됩니다.

* web.xml 소스 코딩 확인
1단계) WEB-INF 폴더 안에 web.xml 소스 코딩
2단계) <location> 태그에 지정한 에러 페이지는 일반 JSP와 동일하게 작성하면 됩니다.
         source05폴더 안에 error 폴더 안에 error404.jsp 파일을 소스 코딩합니다.
         그리고, source05폴더 안에 error 폴더 안에 error500.jsp 파일을 소스 코딩합니다.

* 주요 HTTP 프로토콜 응답 상태 코드
HTTP 프로토콜은 응답 상태 코드를 이용해서 서버의 처리 결과를 웹 브라우저에 알려줍니다.
주요 응답 상태 코드로는 다음과 같은 것들이 있습니다.
- 200 : 요청을 정상적으로 처리함
- 307 : 임시로 페이지를 리다이렉트함
- 400 : 클라이언트의 요청이 잘못된 구문으로 구성됨
- 401 : 접근을 허용하지 않음
- 404 : 요청한 니RL을 처리하기 위한 자원이 존재하지 않음
- 405 : 요청한 메서드(GET: POST, HEAD 등의 전송 방식® 허용하지 않음
- 500 : 서버 내부 에러가 발생함(예를 들어, JSP에서 익셉션이 발생함)
- 503 : 서버가 일시적으로 서비스를 제공할 수 없음
         (급격하게 부하가 몰리거나 서버가 임시 보수 중인 경우가 해당)

JSP가 정상적으로 실행되는 경우 응답 코드로 200이 전송되며,
response.sendRedirect()를 이용할 경우 응답 코드로 307을 전송합니다.
HTTP 응답 코드는 "https://ko.wikipedia.org/wiki/HTTP_상태_코드" 웹사이트에서 확인할 수 있습니다.

5. 익셉션 타입별로 에러 페이지 지정하기
JSP 페이지에서 발생하는 익셉션 종류별로 에러 페이지를 지정할 수도 있습니다.
이것은 앞서 실습했던 에러 코드별로 에러 페이지를 지정하는 방법과 유사합니다.
다음과 같이 <error-code> 태그 대신에 〈exception-type〉태그를 사용하면 됩니다.

* source05 폴더 안에 WEB-INF 폴더 안에 web.xml 파일 소스 추가 코딩

〈error-page〉
   <exception-type> java.lang.NullPointerException </exception—type〉
   <location>/error/errorNullPointer.jsp</location>
〈/error - page〉

위 코드는 JSP 페이지에서 NullPointerException이 발생할 경우
errorNullPointer.jsp를 에러 페이지로 보여준다는 것을 의미합니다.

* source05 폴더 안에 error 폴더 안에 errorNullPointer.jsp 파일 소스 코딩

* source05 폴더 안에 readParameter2.jsp 파일 소스 코딩
   - name 파라미터를 전달하지 않고 실행 확인함.
   그러면, NullPointerException이 발생함.

[참고 내용 : 에러 페이지의 우선순워와 에러 페이지 지정 형태]
지금까지 에러 페이지를 지정하는 3가지 방법에 대해서 실습 했습니다.
에러 페이지를 여러 방법으로 지정한 경우 다음의 우선순위에 따라 사용할 에러 페이지를 선택합니다.
1. page 디렉터브의 errorPage 속성에 지정한 에러 페이지를 보여줍니다.
2. JSP 페이지에서 발생한 익셉션 타입이 web.xml 파일의〈exception-type〉에 지정한
  익셉션 타입과 동일한 경우 지정한 에러 페이지를 보여줍니다.
3. 에러 코드가 web.xml 파얼의〈error-code〉에 지정한 에러 코드와 동일한 경우
   지정한 에러 페이지를 보여줍니다.
4. 아무것도 해당하지 않는 경우 웹 컨테이너가 제공하는 기본 에러 페이지를 보여줍니다.

* 우선순위를 고려해서 다음과 같이 에러 페이지를 지정합니다.
- 전용 에러 페이지가 필요한 경우 page 디렉터브의 errorPage 속성을 사용해서
  에러 페이지를 지정합니다.
- 범용적인 에러 코드(404, 500 등)에 대해 web.xml에 에러 페이지를 지정합니다.
- 별도로 처리해야 하는 익솁션 타입(심각함을 나타내는 익솁션)에 대해서는
  web.xml에 <exception-type> 태그를 추가해서 에러 페이지를 지정합니다.