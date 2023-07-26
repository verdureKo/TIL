# JSTL 표준 태그 라이브러리

JSP는 <jsp:include>와 같은 태그를 개발자가 추가할 수 있는 기능을 제공하는데 이
를 커스텀 태그라고 합니다. 커스텀 태그 중에서 많이 사용되는 것들을 모아서
JSTL(JSP Standard Tag Library)이라는 표준을 만들었습니다.
이 표준 태그 라이브러리를 사용하면 스크립트릿 코드의 사용을 줄이면서
더욱 간결하고 이해하기 쉬운 JSP 코드를 작성할 수 있습니다.

1. JSTL 이란?
JSP는 스크립트릿과 표현식 등의 스크립트 코드와 HTML 코드가 뒤섞이게 되는데,
이렇게 뒤섞인 JSP 코드는 알아보기가 쉽지 않습니다.

JSP는 실행 코드와 화면을 구성하는 HTML 코드를 쉽게 섞을 수 있어서
개발이 편리하지만, 반대로 스크립트 코드와 HTML 코드가 섞이면서
코드의 가독성은 나빠집니다.

HTML 태그와 비슷한 태그를 사용해서 반복문이나 조건문을 처리할 수 있다면,
스크립트 코드를 사용할 때보다 보기 좋고 이해하기 쉬운 코드를 작성할 수 있을 것입니다.

JSP는 새로운 태그를 추가할 수 있는 기능을 제공하고 있는데,
이것이 바로 커스텀 태그(Custom tag)입니다.
JSP는 <jsp:include〉나 <jsp:useBean>과 같은 액션 태그를 제공하는데,
이들은 특수한 기능을 수행합니다. 이와 비슷하게 커스텀 태그도 특수한 기능을
수행하도록 작성할 수 있습니다.

JSP 페이지에서 많이 사용되는 논리적인 판단, 반복 처리, 포맷 처리를 위한 커스텀 태
그를 표준으로 만들어서 정의한 것이 있는데, 그것이 바로 JSTL(JSP Standard Tag Library) 입니다.

JSP 2.3과 호환되는 JSTL 버전은 1.2이며, 우리는 JSTL 1.2 버전을 기준으로
사용방법을 살펴보도록 하겠습니다. 참고로 JSTL 1.2 버전은 JSP 2.2와 2.1과도 호환이 됩니다.

[중요 : 중요) jstl라이브러리 받아서 lib 폴더에 넣기.txt 파일 참고 바랍니다]
※ jstl라이브러리 받아서 lib 폴더에 넣기

1단계) 구글에서 jstl-1.2.jar 검색
2단계) Maven Repository 선택
3단계) JSTL>>1.2에서 Files -> jar(404KB) 클릭 다운로드
4단계) WEB-INF 폴더 안에 lib 폴더 안에 jstl-1.2.jar 파일을 넣어줌
5단계) 톰캣 재시작

[참고 사항]
jstl 1.0 버전은 jstl-1.0.2.jar과 standard-1.0.6.jar과 같이
2개의 jar 파일을 라이브러리로 활용 했습니다.

===================================================================

1) JSTL이 제공하는 태그의 종류
JSTL 1.2는 다음과 같이 5가지 종류의 태그를 제공하고 있습니다.
[다음]
라이브러리  	   주요 기능		    접두어   	관련 URI
 코어(core)         변수지원, 흐름 제어, URL 처리           c	    http://java.sun.com/jsp/jstl/core
 XML(xml)          XML 코어, 흐름 제어, XML 변환         x	    http://java.sun.com/jsp/jstl/xml
국제화(fmt)        지역, 메시지 형식, 숫자 및 날짜 형식  fmt   http://java.sun.com/jsp/jstl/fmt
데이터베이스(sql)  	     SQL	                                 sql   http://java.sun.com/jsp/jstl/sql
 함수(fn)	          컬렉션 처리, String 처리	         fn	    http://java.sun.com/jsp/jstl/functions

[중요]
코어(jstl core) : https://docs.oracle.com/javaee/5/jstl/1.1/docs/tlddocs/c/tld-summary.html
XML(jstl xml) : https://docs.oracle.com/javaee/5/jstl/1.1/docs/tlddocs/x/tld-summary.html
국제화(jstl fmt) : https://docs.oracle.com/javaee/5/jstl/1.1/docs/tlddocs/fmt/tld-summary.html
데이터베이스(jstl sql) : https://docs.oracle.com/javaee/5/jstl/1.1/docs/tlddocs/sql/tld-summary.html
함수(jstl fn) : https://docs.oracle.com/javaee/5/jstl/1.1/docs/tlddocs/fn/tld-summary.html

위에 5가지 종류의 커스텀 태그 중에서, 코어 라이브러리(jstl core), 국제화 라이브러리(jstl fmt),
함수 라이브러리(jstl fn)를 많이 사용합니다.

접두어는 JSP 페이지가 커스텀 태그를 호출할 때 사용합니다.
위의 [다음]에서 접두어는 JSTL에 대해 일반적으로 사용하는 것들입니다.
위의 [다음]에서 접두어가 아닌 다른 문자열을 사용하더라도 상관없습니다.
관련 URI는 JSTL이 제공하는 커스텀 태그를 구분해주는 식별자입니다.
이 식별자를 이용해서 JSP 페이지에서 사용할 커스텀 태그 라이브러리를 선택할 수 있습니다.

2) JSTL 라이브러리 받기
JSTL을 사용하려면 JSTL 1.2 버전을 구현한 jar 파일을 다운로드해야 합니다.

* 다음의 웹사이트에서 다운로드 받기 : Files - jar(404kb) 클릭 다운로드
  https://mvnrepository.com/artifact/javax.servlet/jstl/1.2

① 구글 검색 : jstl-1.2.jar
② Maven Repository 선택
③ JSTL >> 1.2에서 Files
④ jar 클릭 다운로드
⑤ WEB-INF 폴더 안에 lib 폴더 안에 jstl-1.2.jar 파일 넣어주고, 톰캣 서버 재시작해 줌!

참고로, JSTL 1.2는 JSP 2.1 이상을 지원하는 웹 컨테이너를 요구하기 때문에
톰켓 6이상 버전이나 JSP 2.1 또는 그 이상을 지원하는 컨테이너에서 사용해야 합니다.

2. 코어 태그
코어 태그 라이브러리는 변수 설정이나 if-else와 같은 논리 처리에 사용되는
스크립트 코드를 대체하는 태그를 제공합니다. 관련 태그는 다음과 같습니다.
[다음] 코어 태그 라이브러리
 기능 분류     태그               의미
 변수 지원      set	      JSP에서 사용할 변수를 설정합니다.

	    remove    설정한 변수를 제거합니다.
 흐름 제어       if	      조건에 따라 내부 코드를 수행합니다.
	    choose     다중 조건을 처리할 때 사용됩니다.
	    forEach     컬렉션이나 Map의 각 항목을 처리할 때 사용됩니다.
	   forTokens   구분자로 분리된 각각의 토큰을 처리할 때 사용됩니다.

	    import      URL을 사용하여 다른 자원의 결과를 삽입합니다.
 URL 처리   redirect     지정한 경로로 리다이렉트 합니다.
	      url	      URL을 재작성 합니다.

 기타 태그    catch	      익셉션을 처리할 때 사용합니다.
	     out         JspWriter에 내용을 출력합니다.

코어 태그 라이브러리를 사용하려면 JSP 페이지에 다음과 같이 taglib 디렉터브를
추가해야 한다.
<%@ taglib prefix=”c” uri="http//java.sun.com/jsp/jstl/core" %>
prefix 속성에 지정한 값은 JSP 코드에서 코어 태그 라이브러리를 호출할 때 사용할
접두어가 됩니다. uri 속성값은 http://java.sun.com/jsp/jstl/core인데,
이 URI는 위에 [다음]에서 보여준 URI와 동일한 것을 알 수 있습니다.

1) 변수 지원 태그
변수 지원 태그는 JSTL이 지원하는 태그에서 사용할 수 있는 변수를 설정하기 위해
사용 합니다. 변수 지원 태그에는 set 태그와 remove 태그가 있습니다.
① <c：set> 태그
<c：set> 태그는 EL 변수의 값이나 EL 변수의 프로퍼티 값을 지정할 때 사용 됩니다.
<c：set> 태그의 첫 번째 사용방법은 EL 변수를 생성하는 것으로서 형식은 다음과 같습니다.
[다음]
〈c:set var="변수명" value:"값" [scope="영역"] />
〈c:set var=”변수명" [scope:"영역"]〉값〈/c:set〉
위 형식에서 각 속성은 다음과 같은 의미를 갖고 있습니다.
• var : 값을 저장할 EL 변수의 이름을 지정합니다.
• value : 변수의 값을 지정합니다. 표현식, EL, 정적인 텍스트를 사용해서 값을 지정할 수 있습니다.
• scope : 변수를 저장할 영역을 지정합니다. 값은 page, request, session, application 중 하나가 옵니다.
            지정하지 않으면 page를 기본값으로 사용 합니다.
<c：set> 태그는 scope 속성에서 지정한 영역에 값을 저장 합니다.
예를 들어, scope 속성이 page이고 var 속성과 value 속성이 각각 "varName"과 "varValue"라고 하면,
이 경우, 내부적으로 pageContext.setAttribute(varName, varValue, scope)를 호출해서
지정한 영역의 속성으로 설정합니다.

* JSP 소스 코딩 : source10 폴더 안에 core_set.jsp 소스 코딩

* 프로퍼티 값을 설정할 때 사용되는 각 속성은 다음과 같습니다.
• target : 프로퍼티 값을 설정할 대상 객체를 지정합니다. 표현식(〈%= 변수 %〉)이나
            EL 변수(${varName})를 사용할 수 있습니다. 대상 객체는 자바빈 객체나 Map이어야 합니다.
• property : 설정할 프로퍼티의 이름을 지정합니다. target이 자바빈 객체인 경우 프로퍼티
               이름에 해당하는 set 메서드를 제공해야 합니다. 예를 들어, 프로퍼티 이름이
               name인 경우 target 객체는 setName() 메서드를 제공해야 합니다.
               Map인 경우 Map.put(프로퍼티이름, 값)을 이용해서 값을 설정합니다.
• value : 프로퍼 티의 값을 지정합니다.

* JAVA 소스 코딩 : source10\WEB-INF\src\jstl 폴더 안에 MemberVO.java 소스 코딩
* JSP 소스 코딩 : source10 폴더 안에 core_set_target.jsp 소스 코딩

* 다음은 <c：set> 태그의 속성에 대한 설명을 요약한 것입니다.
[다음]

  속성	      표현식/EL	 티입	     의미
  var	      사용 불가	String	EL 변수 이름
  value	      사용가능	Object	변수에 할당할 값
  scope	      사용 불가 	String	변수를 생성할 영역, 기본값은 page
  target	      사용가능	Object	프로퍼티 값을 설정할 객체 지정
  property     사용가능	String	프로퍼티 이름

② <c：remove> 태그
remove 태그는 set 태그로 지정한 변수를 삭제할 때 사용합니다. 구문은 다음과 같습니다.

〈c:remove var="varName" [scope="영역"] />
var 속성과 scope 속성은 set 태그의 두 속성과 동일한 의미를 갖습니다.
remove 태그를 사용할 때 주의할 점은 삭제할 변수의 scope를 지정하지 않으면
동일한 이름으로 저장된 모든 영역의 변수를 삭제한다는 점입니다.

* 다음은 〈c:remove> 태그의 속성에 대한 설명을 요약한 것입니다.
[다음]
  속성	  표현식/EL	타입	       의미
  var	  사용 불가	String	삭제할 EL 변수 이름
  scope	  사용 불가	String	삭제할 변수가 포함된 영역	

2) 흐름 제어 태그
JSTL에서 많이 사용되는 태그 중 하나는 흐름 제어 태그 입니다. JSP에서 스크립트 코드로
if-else 블록이나 for 반복문 등을 조금만 중첩해서 사용해도 〈%, %>, {, } 등이 복잡하게
얽히는데, 이는 개발자가 코드를 이해하는 데 방해 됩니다. 이런 코드의 복잡함을 없애기 위해
JSTI은 흐름 제어를 처리할 수 있는 태그를 제공 합니다. JSTL이 제공하는 흐름 제어 태그는
if, choose, forEach, forTokens 네 개가 있습니다.

① <c：if> 태그
if 태그는 이름에서 알 수 있듯이 자바 언어의 if 블록과 비슷한 기능을 제공 합니다.
중첩된 if-else 블록과 같은 효과를 낼 순 없지만 단순한 if 블록을 쉽게 대체할 수 있기 때문에
많이 사용 합니다. 사용방법은 다음과 같습니다.
[다음]
<c:if test="조건">
...
</c:if>
test 속성은 true나 false에 해당하는 값이 옵니다. 이 조건 값이 true이면 <c:if> 태그의
몸체 내용을 처리 합니다. test 속성은 표현식이나 EL 또는 정적 문자열을 값으로 가질 수
있습니다. Deferred Expression(#{expr})은 값으로 가질 수 없습니다.

* JSP 소스 코딩 : <c:if> 태그 사용 예시 : source10 폴더 안에 use_if_tag.jsp 소스 코딩

* 다음은 <c:if> 태그의 속성에 대한 설명을 요약한 것입니다.
[다음]
  속성	  표현식/EL       타입	    의미
  test	사용 가능	     boolean	검사 조건
  var	사용 불가	     String	검사 조건의 계산 결과값을 저장할 EL 변수
  scope	사용 불가	     String	if 결과를 저장할 EL 변수의 영역

② <c:choose>, <c:when>, <c:otherwise> 태그
<c:choose> 태그는 자바의 switch 구문과 if-else 블록을 혼합한 형태로서
다수의 조건문을 하나의 블록에서 수행할 때 사용합니다.

* JSP 소스 코딩 : source10 폴더 안에 use_choose_tag.jsp 소스 코딩

③ <c:forEach> 태그
forEach 태그는 배열, Collection 또는 Map에 저장되어 있는 값들을
순차적으로 처리할 때 사용 합니다. 자바의 for, do-while 등을 대신해서
사용할 수 있습니다.  forEach 태그의 기본적인 사용방법은 다음과 같습니다.
[다음]
<c:forEach var="변수” items="아이템">
...
〈tr〉
  <td align="right” bgcolor=”#ffffff">
  ${변수사용}
  </td>
...
</c:forEach>

items 속성에는 Map, 배열, Collection이 올 수 있습니다. 배열의 경우는
객체의 배열뿐만 아니라 기본 데이터 타입의 배열에 대해서도 알맞게 처리를 하며,
기본 데이터 타입은 Integer나 Double과 같은 래퍼 클래스를 사용해서 처리하게 됩니다.
그리고, forEach 태그를 사용해서 자바의 for 구문과 같은 효과를 낼 수도 있습니다.

* JSP 소스 코딩 : source09 폴더 안에 use_foreach_tag.jsp 파일 소스 코딩

다음은 <c:forEach> 태그의 속성에 대한 설명을 요약한 것입니다.
[다음]
 속성	  표현식/EL           타입	                            의미
  var	   사용 불가  	String	               몸체에서 사용할 EL 변수 이름

 items	   사용 가능         Collection, Iterator,   반복 처리할 데이터
                                    Enumeration,
                                    Map, 배열	

 varStatus  사용 불가	String	               루프 상태를 저장할 EL 변수 이름
 begin	  사용 가능	int	               시작 인덱스 값
 end	  사용 가능	int	               끝 인덱스 값
 step	  사용 가능	int	               인덱스 증분 값

④ <c:forTokens> 태그
forTokens 태그는 java.util.StringTokenizer 클래스와 같은 기능을 제공하는 태그로서
기본 형식은 다음과 같습니다.
[다음]
〈c:forTokens var="token" items="문자열" delims="구분자"〉
${token}의 사용
〈/c:forTokens〉

<c：foiTokens> 태그는 items 속성으로 전달받은 문자열을 구분자를 이용해서 나누고,
구분한 각 문자열을 var 속성에 명시한 변수에 저장합니다.
<c:forTokens> 태그는 <c:forEach> 태그와 동일하게 begin, end, step, varStatus 속성을
제공합니다. 아울러, <c:forTokens> 태그의 items 속성값이 String이라는 것을 제외하면,
나머지 <c:forTokens> 태그의 속성은 <c:forEach> 태그의 속성과 동일 합니다.

* JSP 소스 코딩 : 콤마(", ")와 점을 구분자로 사용해서 문자열에서 토큰을 추출하는 예시
[source10 폴더 안에 use_fortokens_tag.jsp 소스 코딩]

3) URL 처리 태그
URL 관련 태그는 다음의 두 가지 기능을 제공합니다.
• URL 생성 : <c:url> 태그
• 리다이렉트 처리 : <c:redirect> 태그

<c:url> 태그 = URL을 생성해주는 기능을 제공합니다. 기본 사용방법은 다음과 같습니다.
[다음]
<c:url value="URL" [var="varName"][scope="영역"]>
   <c:param name="이름" value="값" />
</c:url>
var 속성과 scope 속성은 생략 가능 합니다. var 속성을 지정하지 않으면 현재 위치에
생성한 URL을 출력하며, var 속성을 지정하면 해당 변수에 생성한 URL을 저장합니다.
<c:param> 태그를 이용해서 파라미터를 URL에 추가할 수 있습니다.
value 속성은 다음과 같이 절대 URL과 상대 UBL의 두 가지 방식으로 입력할 수 있습니다.
• 절대 URL : http://www.kbs.co.kr 같은 완전한 URL
• 상대 URL
 - 웹 어플리케이션 내에서의 절대 경로 : 슬래시로 시작. 예) /view/list.jsp
 - 현재 JSP에 대한 상대 경로 : 슬래시로 시작하지 않음. 예）../view/list.jsp
웹 어플리케이션 내에서의 절대 경로를 사용할 경우 실제로 생성되는 URL은 컨텍스트
경로를 포함 합니다.

* JSP 소스 코딩 : source10 폴더 안에 use_url_tag.jsp 소스 코딩


3. 국제화 태그
국제화 태그(fmt)는 특정 지역에 따라 알맞은 메시지를 출력해야 할 때 사용합니다.
예를 들어, 한글 브라우저에서 접속하면 한글 메시지를 출력하고 영문 브라우저에서
접속하면 영문 메시지를 출력해야 할 때 국제화 태그를 사용합니다.
이런 기능을 제공하기 위해 언어마다 별도의 JSP 페이지를 작성해야 한다면 개발자는
똑같은 JSP 페이지를 복사하고 수정하느라 시간을 다 보내게 될 것입니다. JSTL은 이런
중복 작업을 덜고 하나의 JSP 페이지에서 다양한 언어에 맞는 메시지를 출력할 수 있도록
해주는 태그를 제공하고 있습니다. 이들 태그는 다음과 같습니다.
[다음]
기능분류	 	   태그	                     의미
로케일(위치) 지정	  setLocale	  Locale을 지정합니다.
	              requestEncoding	  요청 파라미터의 캐릭터 인코딩을 지정합니다.

메시지 처리	  bundle	              사용할 번들을 지정합니다.
	              message	  지역에 알맞은 메시지를 출력합니다.
	              setBundle	  리소스 번들을 읽어와 특정 변수에 저장합니다.

숫자 및 날짜 포맷팅  formatNumber	숫자를 포맷팅 합니다.
	              formatDate	Date 객체를 포맷팅 합니다.
	              parseDate	문자열로 표시된 날짜를 분석해서 Date 객체로 변환합니다.
	              parseNumber	문자열로 표시된 날짜를 분석해서 숫자로 변환합니다.
	              setTimeZone	시간대 정보를 특정 변수에 저장합니다.
	              timeZone	시간대를 지정합니다.

1) <fmt:formatDate> 태그
<fmt:formatDate> 태그는 날짜 정보를 담고 있는 객체를 포맷팅하여 출력할 때 사용하며, 사용 형식은 다음과 같습니다.
[다음]
<fmt:formatDate value="날짜값"
    [type="타입"] [dateStyle="날짜스타일] [timeStyle="시간스타일"]
    [pattern="패턴"] [timeZone="타임존"]
    [var="변수명"] [scope="영역"] />

<fmt:formatDate> 태그의 각 속성은 다음과 같습니다.
  속성  	  표현식/EL	타입	         의미
  value	  사용가능	java.util Date  포맷팅할 시간 값을 지정합니다.

  type	  사용가능           String	      날짜, 시간 또는 둘 다 포맷팅할지 여부를 지정합니다.
                                                      time, date, both 중 한 가지 값을 가질 수 있으며,
                                                      기본값은 date 입니다.

 dateStyle  사용가능	String	      날짜에 대해 미리 정의된 포맷팅 스타일을 지정합니다.
                                                      default, short, medium, Long, full 중 한 가지 값을 가질 수 있으며,
                                                      기본값은 default입니다.

 timeStyle  사용가능	String	       시간에 대해 미리 정의된 포맷팅 스타일을 지정합니다.
                                                       default, short, medium, long, full 중 한 가지 값을 가질 수 있으며,
                                                       기본값은 default 입니다.
[dateStyle 및 timeStyle 참고 사항]
dateStyle 및 timeStyle에서 사용되는 full, medium, long 등의 값이 실제로 어떤 포맷으로 값을
출력하는지에 대한 내용은 DateFormat 클래스에 대한 API 문서(아래 URL)를 참고 바랍니다.
http://docs.oracle.com/javase/8/docs/api/java/text/SimpleDateFormat.html

  pattern	  사용가능	String	       직접 파싱할 때 사용할 양식을 지정합니다.
                                                        java.text.DateFormatoil 있는 양식을 사용합니다.

 timeZone  사용가능	String 또는         시간대를 변경하고 싶을 때 사용합니다.
                                    java.util.TimeZone <fmt:setTimeZone> 태그에서 생성한 TimeZone 객체를 사용합니다.
                                    	
    var	  사용불가	String	           파상한 결과를 저장할 변수명을 지정합니다.
  scope	  사용불가	String	           변수를 저장할 영역을 지정합니다. 기본값은 page입니다.


* JSP 소스 코딩 : <fmt:formatDate> 태그는 다양하게 날짜 및 시간을 출력할 수 있도록 해줍니다.
[source10 폴더 안에 use_date_tag.jsp 소스 코딩]

2) <fmt:parseDate> 태그
<fmt:parseDate> 태그는 문자열로 표시된 날짜와 시간 값을 java.util.Date로 파싱해 주는
기능을 제공합니다. <fmt:parseDate> 태그의 사용 형식은 다음과 같습니다.
[다음]
<fmt:formatDate value="날짜값"
  [type="타입"][dateStyle="날짜스타일"] [timeStyle="시간스타일"]
  [pattern="패턴"] [timeZone="타임존"] [parseLocale="로케일"]
  [var="변수명"] [scope="영역"] />

<fmt:parseDate> 태그의 각 속성은 다음과 같습니다.
 속성	 표현식/EL	타입	       의미
 value	 사용가능	           String	파상할 문자열을 지정합니다.

 type	 사용가능	           String	날짜, 시간 또는 둘 다 포맷팅할지 여부를 지정합니다.
                                                time, date, both 중 한 가지 값을 가질 수 있으며, 기본값은 date입니다.

dateStyle	 사용가능           String	날짜에 대해 미리 정의된 포맷팅 스타일을 지정합니다.
                                                default, short, medium, long, full 중 한 가지 값을 가질 수 있으며,
                                                기본값은 default입니다.

timeStyle	 사용가능            String	시간에 대해 미리 정의된 포맷팅 스타일을 지정합니다.
                                                default, short, medium, long, full 중 한 가지 값을 가질 수 있으며,
                                                기본값은 default입니다.

pattern	사용가능	            String	직접 파싱할 때 사용할 양식을 지정합니다.
                                                 java.text.DateFormat에 있는 양식을 사용합니다.

timeZone	 사용가능	            String 또는          시간대를 변경하고 싶을 때 사용합니다.
                                    java.util.TimeZone	<fmt:setTimeZone> 태그에서 생성한 TimeZone 객체를 사용합니다.

parseLocale  사용가능	String 또는 java.util.Locale	파싱할 때 사용할 로케일을 지정합니다.
var	    사용불가	String	                        파싱한 결과를 저장할 변수명을 지정합니다.
scope	    사용불가	String	                        변수를 저장할 영역을 지정합니다. 기본값은 page입니다.

다음 코드는〈fmt:parseDate>의 사용 예를 보여주고 있습니다.
[다음]
<fmt:parseDate value=’’2022-03-01 13:00:59”
              pattern="yyyy-MM-dd HH:mm:ss" var="date" />
${date}

3) <fmt:timeZone> 태그와 <fmt:setTimeZone> 태그
날짜와 시간에는 시간대라는 것이 존재 합니다. 한국 시간과 미국 LA의 시간은 차이가 나며,
시간대별로 권역을 묶어 같은 시간을 사용하고 있습니다. JSTL 포맷팅 태그도
시간대별로 시간을 처리할 수 있는 기능을 제공하는데 이때 사용되는 태그가 바로
<fmt:timeZone>태그와 <fmt:setTimeZone> 태그 입니다.
먼저 <fmt:timeZone>태그에 대해서 살펴 봅니다. <fmt:timeZone>태그는 value 속성으로
시간대를 입력 받으며 다음과 같이 <fmt:timeZone> 태그 안에서 사용된
<fmt:formatDate> 태그에 영항을 미칩니다.
[다음]
<fmt:timeZone value="Hongkong">
...
  <fmt:formatDate ... /> <!-- 사용하는 시간을 Hongkong 시간대에 맞춥니다 -->
...
</fmt: timeZone>

* JSP 소스 코딩 : 시간을 현재 시간과 홍콩 시간의 두 가지로 출력하기 위해 <fmt:timeZone> 태그 사용 예시
[source10 폴더 안에 use_timezone_tag.jsp 소스 코딩] (참고로, 홍콩은 한국보다 1시간 느립니다)

* JSP 소스 코딩 : timeZone 태그의 value 속성에는 String이나 TimeZone 객체를 값으로 줄 수 있습니다.
  만약 value 속성에 문자열로 값을 주고 싶다면 java.util.TimeZone 클래스를 이용해서 시간대를 표현하는
  문자열 값을 구할 수 있습니다. 이번에는 TimeZone 클래스를 사용해서 사용 가능한 시간대 목록을 출력해주는
  코드를 작성해 봅니다.
[source10 폴더 안에 listTimeZones.jsp 소스 코딩 - 실행 확인은 Chrome 실행 후 마우스 우클릭
                                - 페이지 소스 보기에서 Ctrl+F키 → Hongkong 검색 확인
                                (즉, 웹브라우저 인식 소스 코딩 내용 비교 확인함)]

[참고 사항] web.xml 파일에 국제화 관련 태그 기본값 설정하기
웹 어플리케이션이 기본으로 사용할 로케일 정보나 시간대를 web.xml 파일에 컨텍스트
초기화 파라미터를 이용해서 설정할 수도 있습니다. 이들 "국제화 관련 컨텍스트 초기화 파라미터"는
다음과 같습니다.
[다음]
  속성 이름	                                                    의미
javax.servlet.jsp.jstl.fmt.localizationContext    기본으로 사용할 리소드 번들을 지정합니다.
                                                        리소스 번들의 basename을 입력합니다.
javax.servlet.jsp.jstl.fmt.locale	                    기본으로 사용할 로케일을 지정합니다.
javax.servlet.jsp.jstl.fmt.timeZone	        기본으로 사용할 시간대를 지정합니다.


4. 함수(functions : fn)
JSTL은 표현 언어에서 사용할 수 있는 함수를 제공하고 있습니다. EL에서 객체의 메서드를
직접 호출할 수 있게 되면서 효용성이 다소 떨어졌지만, 이런 것이 있다는 정도는 알고
넘어가도록 합니다. JSTL이 제공하는 EL 함수는 다음과 같습니다.
[다음]
속성 이름		                                        의미
length(obj)	         obj가 List와 같은 Collection인 경우 저장된 항목의 개수를 리턴하고,
                                 obj가 문자열일 경우 문자열의 길이를 리턴합니다.

toUpperCase(str)	         str을 대문자로 변환 합니다.
toLowerCase(str)	         str을 소문자로 변환 합니다.
substring(str, idx1, idx2)    str.substring(idx1, idx2)의 결과를 리턴합니다.
                                 idx2가 -1 일 경우 str.substring(idx1)과 동일합니다.

substringAfter(str1, str2)	   str1에서 str1에 포함되어 있는 str2 이후의 문자열을 구합니다.
substringBefore(str1, str2)	   str1에서 str1에 포함되어 있는 str2 이전의 문자열을 구합니다.
trim(str)                        	   str 좌우의 공백문자를 제거합니다.
replace(str, src, dest)	   str에 있는 src를 dest로 변환합니다.
indexOf(str1, str2)	               str1에서 str2가 위치한 인덱스를 구합니다.
startsWith(str1, str2)	   str1이 str2로 시작할 경우 true를, 그렇지 않을 경우 false를 리턴합니다.
endsWith(str1, str2)	   str1이 str2로 끝나는 경우 true를, 그렇지 않을 경우 false를 리턴합니다.
contains(str1, str2)	               str1 이 str2를 포함하고 있을 경우 true를 리턴합니다.
containslgnoreCase(str1, str2)  대소문자 구분 없이 str10| str2를 포함하고 있을 경우 true를 리턴합니다.
split(str1, str2)	               str2로 명시한 글자를 기준으로 str1 을 분리해서 배열로 리턴합니다.
join(array, str2)	               array에 저장된 문자열을 합칩니다. 이때 각 문자열 사이에는 str2가 붙습니다.
escapeXml(str)	               XML의 객체 참조에 해당하는 특수 문자를 처리합니다.
                                       예를 들어, '&'는 '&amp;'로 변환합니다.

* JSP 소스 코딩 : 함수를 사용한 예시를 소스 코딩 후 실행 결과를 통해 각 함수가 어떻게 동작하는지
                     확인하시기 바랍니다.
[source10 폴더 안에 use_function.jsp 소스 코딩 - 실행 확인]

1단계) 구글에서 jstl-1.2.jar 검색
2단계) Maven Repository 선택
3단계) JSTL>>1.2에서 Files -> jar(404KB) 클릭 다운로드
4단계) WEB-INF 폴더 안에 lib 폴더 안에 jstl-1.2.jar 파일을 넣어줌
5단계) 톰캣 재시작

[참고 사항]
jstl 1.0 버전은 jstl-1.0.2.jar과 standard-1.0.6.jar과 같이
2개의 jar 파일을 라이브러리로 활용 했습니다.