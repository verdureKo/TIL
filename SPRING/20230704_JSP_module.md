# JSP 페이지 모듈화와 요청 흐름 제어

1. <jsp：include> 액션 태그를 이용한 공통 영역 작성
보통 하나의 웹 사이트를 구성하는 페이지들은 동일한 상단 메뉴,
좌측 메뉴 그리고 하단 푸터를 갖고 있습니다.
이런 공통 구성 요소를 위한 코드를 모든 JSP 페이지마다 작성한다면
코드 중복이 발생하게 됩니다. 게다가 공통 구성 요소의 일부를 수정하려면
모든 JSP 페이지를 수정해야 하는 부담도 있습니다.
이런 화면 구성 요소의 코드 중복 문제를 없앨 때 사용 할 수 있는 것이 바로
<jsp：include> 액션 태그입니다.
<jsp：include> 액션 태그는 위치한 부분에 지정한 페이지를 포함합니다.

["그림_1) jsp include 액션 태그의 동작 방식.pdf" 참고]

1) <jsp：include> 액션 태그 사용범
<jsp:include> 액션 태그의 기본 사용방법은 다음과 같습니다.
[다음]
<jsp:include page= "포함할페이지" flush="true" /〉

<jsp:include> 액션 태그의 두 속성은 다음과 같습니다.
[다음]
① page : 포함할 JSP 페이지의 경로를 지정합니다.
② flush : 지정한 JSP 페이지를 실행하기 전에 출력 버퍼를 플러시할지 여부를 지정합니다.
   true이면 출력 버퍼를 플러시하고, false이면 플러시하지 않습니다. 기본값은 false입니다.

* JSP 소스 코딩 : <jsp:include> 액션 태그의 동작 방식을 이해하기 위한 예시
[source06 폴더 안에 main.jsp 소스 코딩]
[source06 폴더 안에 sub.jsp 소스 코딩]

main.jsp에서는 <jsp:include> 액션 태그를 사용하여 sub.jsp를 포함시키고 있습니다.

2) <jsp:include> 액션 태그를 이용한 중복 영역 처리
공통 영역을 사용하려는 JSP 페이지는 <jsp：include> 액션 태그를 사용해서
공통 영역을 포함할 수 있습니다. 공통 영역을 생성하는 코드가
한 개의 JSP 페이지에 위치하므로, 공통 영역을 위한 코드가 중복되는
것을 방지할 수 있습니다.

* JSP 소스 코딩 : <jsp:include> 액션 태그를 사용하여 페이지의 공통 부분을 읽어오는 예시
[source06 폴더 안에 layout.jsp 소스 코딩]
[source06 폴더 안에 module 폴더 안에 top.jsp, left.jsp, bottom.jsp 소스 코딩]
layout.jsp는 상당(top.jsp), 좌측(left.jsp), 하단(bottom.jsp) 영역의 코드를
직접 생성하지 않고, <jsp:include> 액션 태그를 사용하여 관련 영역을 생성하고 있습니다.

3) <jsp:param>으로 포함할 페이지에 파라미터 추가하기
<jsp:include> 액션 태그는 <jsp:param> 태그를 이용해서
포함할 JSP 페이지에 파라미터를 추가할 수 있습니다.
다음 코드는 <jsp:param> 태그의 사용 형식을 보여주고 있습니다.
[다음]
<jsp:include page="/module/top.jsp" flush="false">
    <jsp:param name="param1" value="value1" />
    <jsp:param name="param2" value="value2" />
</jsp:include>

〈jsp:param〉액션 태그는 <jsp:include> 액션 태그의 자식 태그로 추가합니다.
<jsp:param> 액션 태그의 name 속성과 value 속성은 각각 포함할 페이지에
새로 추가할 파라미터의 이름과 값을 입력합니다. value 속성에는
값을 직접 지정하거나 표현식을 이용해서 값을 지정합니다.

〈% String type = "typeA"; %>
<jsp:include page="..." />
   <jsp:param name="name" value="장나라" /> <%-- value에 값을 직접 입력 -->
   <jsp:param name="type" value="<% type %>" /> <%-- 표현식으로 값 입력 -->
</jsp:include>

* JSP 소스 코딩 : 다음은 <jsp:param> 액션 태그를 사용하여
                      infoSub.jsp에 파라미터를 추가로 전달하는 예시입니다.
                      여기서 infoSubj.jsp 페이지는 제품의 타입별로 추가 정보를
                      출력해 주는 화면입니다.
[source06 폴더 안에 info.jsp 소스 코딩]
[source06 폴더 안에 infoSub.jsp 소스 코딩]

[<jsp:param> 액션 태그를 사용할 때 주의할 점]
〈jsp:param〉액션 태그로 추가한 파라미터는 <jsp:include> 액션 태그로
포함하는 페이지에서만 유효하다는 점입니다.

* JSP 소스 코딩 : <jsp:param>을 실행하기 전/후 파라미터 값에
                     변화가 발생하는지 여부를 확인하기 위해 만든 예시이며,
                      body_sub.jsp는 request.getParameter() 메서드와
                      request.getParameterValues() 메서드를 이용해서
                      name 파라미터의 값을 출력합니다.
                      이를 통해 <jsp:param> 태그가 기존 파라미터 값에
                     새로운 값을 추가하는지 여부를 확인할 수 있습니다.
[source06 폴더 안에 body_main.jsp 소스 코딩]
[source06 폴더 안에 body_sub.jsp 소스 코딩]

4) <jsp:param> 액션 태그와 캐릭터 인코딩
앞서, request.setCharacterEncoding() 메서드를 이용해서
요청 파라미터의 캐릭터 셋을 지정하고 있는 것을 알 수 있습니다.

<%
   request.setCharacterEncoding("utf-8");
%>

<jsp：param> 액션 태그는 포함할 페이지에 전달할
요청 파라미터의 값을 인코딩할 때
request.setCharacterEncoding() 메서드로 설정한 캐릭터 셋을 사용합니다.
request.setCharacterEncoding() 메서드로 알맞은 캐릭터 셋을 지정하지 않으면
<jsp:param>으로 설정한 값이 올바르게 전달되지 않게 됩니다.

2. include 디렉티브를 이용한 중복된 코드 삽입
include 디렉티브도 <jsp:include> 액션 태그처럼 지정한 페이지를
현재 위치에 포함시키는 기능을 제공합니다. 
하지만, <jsp:include> 액션 태그와 include 디렉티브는 포함하는 방식에 차이가 있습니다.
<jsp:include> 액션 태그는 다른 JSP로 실행 흐름을 이동시켜
실행 결과를 현재 위치에 포함하는 방식인 반면에,
include 디렉티브는 다른 파일의 내용을 현재 위치에 삽입한 후에
JSP 파일을 자바 파일로 변환하고 컴파일하는 방식입니다.

* include 디렉터브의 사용방법은 다음과 같다.
<%@ include file="포함할파일" %>
file 속성은 include 디렉터브를 사용해서 포함할 파일의 경로를 지정합니다.
include 디렉티브를 사용하면, JSP 파일을 자바 파일로 변환하기 전에
include 디렉티브에서 지정한 파일의 내용을 해당 위치에 삽입하고,
그 결과로 생긴 자바 파일을 컴파일합니다

["그림_2) include 디렉티브의 처리 방식" 참고]

* JSP 소스 코딩 : include 디렉티브 사용 간단한 예시 구현
[source06 폴더 안에 includer.jsp 소스 코딩]

* JSP 소스 코딩 : includer. jsp에서 선언하지 않은 변수인 dataFolder를
   사용하고 있으며, 이 dataFolder 변수를 선언하는 코드는 includee.jspf 파일에 포함되어 있습니다.
[source06 폴더 안에 includee.jspf 소스 코딩 : 참고로, includee.jspf를 includee.jsp로 해도 인식됨]

[includee.jspf를 includee.jsp로 해도 인식 메모]
include 디렉티브를 통해 다른 JSP에 포함되는 JSP 파일의 경우
일반 JSP 파일과 구분하기 위해 확장자로 jspf를 사용하는 편입니다.
물론 확장자로 jsp를 사용해도 됩니다. jspf는 JSP Fragment,
즉, JSP의 소스 코드 조각을 의미합니다.

1) include 디렉티브의 활용
include 디렉터브는 코드 차원에서 다른 JSP를 포함하기 때문에
<jsp:include> 액션 태그와는 다른 용도로 사용합니다.
<jsp:include> 액션 태그가 레이아웃의 한 구성 요소를
모듈화하기 위해 사용되는 반면에, include 디렉터브는
다음의 두 가지 목적으로 주로 사용됩니다.
① 모든 JSP 페이지에서 사용하는 변수 지정 (공통변수 지정)
② 저작권 표시와 같이 모든 페이지에서 중복되는 간단한 문장(중복되는 간단한 문장 구현)

2) <jsp:include> 액션 태그와 include 디렉티브의 비교
<jsp：include> 액션 태그와 include 디렉터브의 차이점은 다음과 같습니다.
[다음]
비교 항목		<jsp:include>			include 디렉티브
처리 시간		요청 시간에 처리			JSP 파일을 자바 소스로 변환할 때 처리
기능		별도의 파일로 요청 처리 흐름을 이동	현재 파일에 삽입시킴
데이터 전달 방법	request 기본 객체나〈jsp:param〉을      페이지 내의 변수를 선언한 후, 변수에 값 저장
                        이용한 파라미터 전달	            다수의 JSP 페이지에서 공통으로 사용되는 
용도		화면의 레이아웃의 일부분을              변수를 지정하는 코드나 저작권과 같은 
                        모듈화할 때 주로 사용함.	            중복되는 간단한 문장을 포함함.

3. <jsp:forward> 액션 태그를 이용한 JSP 페이지 이동
<jsp:forward> 액션 태그는 하나의 JSP 페이지에서 다른 JSP 페이지로
요청 처리를 전달할 때 사용됩니다.

["그림_3) jsp forward의 요청 흐름 처리" 참고]

"그림_3) jsp forward의 요청 흐름 처리"에서는
from.jsp에서 to.jsp로 요청 흐름이 이동하는 것을 보여줍니다.
웹 브라우저의 요청을 최초로 전달받는 것은 from.jsp인데
<jsp:forward>로 인해 다음과 같은 순서로 실행 흐름이 이동합니다.
① 웹 브라우저 요청을 from.jsp에 전달합니다.
② from.jsp는 <jsp:forward> 액션 태그를 실행합니다.
③ <jsp:forward> 액션 태그를 실행하면 요청 흐름이 to.jsp로 이동합니다.
④ 요청 흐름이 이동할 때 from.jsp에서 사용한 request 기본 객체와
    response 기본 객체가 to.jsp로 전달됩니다.
⑤ to.jsp가 응답 결과를 생성합니다.
⑥ to.jsp가 생성한 결과가 웹 브라우저에 전달됩니다.

위에 흐름에서 다음 사실이 중요합니다.
- from.jsp가 아닌 to.jsp가 생성한 응답 결과를 웹 브라우저에 전달합니다.
- from.jsp에서 사용한 request, response 기본 객체를 to.jsp에 그대로 전달합니다.

* 고려 사항 : 왜 from.jsp에서 모든 것을 처리하면 될 것을
  굳이 to.jsp로 요청 흐름을 이동시켜가면서까지 처리하는 것일까요?
  이 질문에 대한 답은 '간결하고 구조적으로 웹/JSP 프로그래밍을 할 수 있기 때문'입니다.
  웹어플리케이션을 개발하다 보면 다양한 조건에 따라 다른 처리를 해야 하는 상황이 발생하는데,
  이럴 때<jsp:forward> 액션 태그를 사용하면 각 조건을 처리하는 JSP를 분리하여
  기능별로 모듈화할 수 있게 됩니다.

1) <jsp:forward> 액션 태그의 사용법
<jsp:forward> 액션 태그의 기본 문법은 다음과 같습니다.
[다음]
<jsp:forward page="이동할 페이지" />
"이동할 페이지"는 웹 어플리케이션 내에서의 경로입니다.

* JSP 소스 코딩 : <jsp:forward> 액션 태그를 사용하는 from.jsp 소스 코딩
[source06 폴더 안에 from 폴더 안에 from.jsp 소스 코딩]

* JSP 소스 코딩 : 위에 from.jsp <jsp:forward> 액션 태그는 to.jsp로 실행 흐름을 이동시키고 있습니다.
[source06 폴더 안에 to 폴더 안에 to.jsp 소스 코딩]

* 실행 결과 분석
- from.jsp에서 <jsp:forward>를 사용해서 이동한 to.jsp가 생성한 결과가
  웹 브라우저에 출력 됩니다.
- 웹 브라우저의 주소는 from.jsp 그대로입니다.
   즉, 리다이렉트처럼 to.jsp로 변경되지 않습니다.

<jsp:forward>는 웹 컨테이너 내에서 요청 흐름을 이동시키기 때문에
웹 브라우저는 다른 JSP가 요청을 처리했다는 사실을 알지 못합니다.
웹 브라우저 주소는 from.jsp로 변경되지 않으므로
웹 브라우저는 from.jsp가 생성한 결과로 인식합니다.
하지만, 실제 출력 결과는 to.jsp가 생성한 것입니다.

2) <jsp:forward> 액션 태그의 활용

* JSP 소스 코딩 : 선택한 옵션에 따라 서로 다른 화면을 보여주는
                      조건 분기 처리 적용 JSP 페이지 소스 코딩
[source06 폴더 안에 select.jsp 소스 코딩]

* JSP 소스 코딩 : select.jsp에서 [이동] 버튼을 누르면 view.jsp로
                     선택한 옵션 값이 전달되는 JSP 소스 코딩
[source06 폴더 안에 view.jsp 소스 코딩]

* JSP 소스 코딩 : view.jsp는 "code" 파라미터의 값에 따라
                      a.jsp, b.jsp, c.jsp로 흐름을 이동시킵니다.
                      각각 이동할 JSP 페이지 소스 코딩
[source06 폴더 안에 viewModule 폴더 안에 a.jsp, b.jsp, c.jsp 소스 코딩]

3_참고만함) <jsp:param> 액션 태그를 이용해서 이동할 페이지에 파라미터 추가하기
<jsp:param> 액션 태그를 사용하면 <jsp:forward> 액션 태그로
이동할 페이지에 파라미터를 추가로 전달할 수 있습니다.
<jsp:forward page="moveTo.jsp">
  <jsp:param name="first” value="NARA" />
  <jsp:param name="last” value="Jang" />
</jsp:forward>
<jsp:param>의 동작 방식은 <jsp:include>에서의 동작 방식과 동일합니다.

4) <jsp:include>와 <jsp:forward> 액션 태그의 page 속성 경로
   OS에 상관없이 경로를 구분할 때에는 '/'를 사용합니다.
   그리고, 절대경로를 주로 사용하는 개발자들은 특별한 경우를 제외하면
   절대 경로를 사용하는데, 그 이유는 절대 경로를 사용하면
   관련 파일을 쉽게 찾을 수 있기 때문입니다.
   그리고, 다음의 경우는 상대 경로를 사용하기도 합니다.
   [다음]
   - 이동할 페이지가 같은 폴더에 위치한 경우
   - 이동할 페이지가 현재 폴더의 하위 폴더에 위치한 경우

4. 기분 객제의 속성올 이용해서 값 전달하기
<jsp:include> 액션 태그와 <jsp:forward> 액션 태그는 <jsp:param> 액션 태그를
이용해서 파라미터를 추가로 전달할 수 있습니다.
하지만, <jsp:param> 액션 태그는 파라미터를 이용해서 데이터를 추가하기 때문에
String 타입의 값만 전달할 수 있다는 제약을 갖고 있습니다.
<jsp:param>은 String 타입의 값만 전달할 수 있기 때문에, 날짜 데이터나 숫자 또는
객체 타입을 파라미터로 전달하려면 값을 문자열로 변환해주어야 하고,
반대로 문자열을 알맞은 타입으로 변환해주는 기능도 구현해야 합니다.

request 기본 객체는 한 번의 요청에 대해 유효하게 동작하며,
한 번의 요청을 처리하는데 사용되는 모든 JSP에서 공유됩니다.

* JSP 소스 코딩 : request 기본 객체에 속성을 추가한 후에
                      <jsp:forward> 액션 태그를 이용해서
                      흐름을 이동시키는 예시 JSP 소스 코딩
[source06 폴더 안에 from 폴더 안에 makeTime.jsp 소스 코딩]

* JSP 소스 코딩 : 위에 makeTime.jsp에서 흐름을 이어 받는
                      viewTime.jsp 소스 코딩
[source06 폴더 안에 to 폴더 안에 viewTime.jsp 소스 코딩]

viewTime.jsp는 request 기본 객체에 저장된 속성인 time 값을 읽어 옵니다.
request 기본 객체의 time 속성은 앞서 makeTime.jsp에서 저장한 것입니다.
makeTime.jsp를 실행하면 현재 시간을 담고 있는 Calendar 객체를 생성해서
request 기본 객체의 time 속성에 저장한 후 viewTime.jsp로 이동합니다.
viewTime.jsp는 request 기본 객체의 time 속성에 저장된 Calendar 객체를 읽어와
현재 시간을 출력 합니다.

앞서, 속성을 이용한 값 전달 방식은 웹 어플리케이션 개발에서 중요한 기법 중 하나입니다.
특히, 이 방식은 MVC(Mode-View-Controller) 패턴이라는 것에 기반하여
웹 어플리케이션을 구현할 때 필수 요소이기 때문에,
request 기본 객체의 속성을 사용하는 방법에 대해서는 반드시 이해하고 넘어가시기 바랍니다.