# EL 표현 언어(Expression Language) 활용

3. EL에서 객체의 메서드 호출
JSP2.2/EL 2.2 버전부터 객체의 메서드를 직접 호출할 수 있습니다.
JSP 2.1 의 경우 EL에서 메서드를 호출하는 EL을 사용하면 에러가 발생했었습니다.
하지만, EL 2.2 버전부터는 메서드를 호출할 수 있습니다.

* JAVA 소스 코딩 : 테스트 자바 클래스 작성
[source09\WEB-INF\scr\source09\Thermometer.java 소스 코딩]

* JSP 소스 코딩 : EL 메서드 호출 지원 확인용 JSP 소스 코딩
[source09 폴더 안에 thermometer.jsp 소스 코딩]

4. EL에서 정적 메서드 호출하기 1
JSP의 표현식은 자바의 클래스를 마음대로 사용할 수 있습니다.
EL은 자바 클래스의 정적 메서드를 호출할 수 있는 두 가지 방법을 제공하고 있습니다.
이 중 첫 번째 방법은 JSP 2.0 버전부터 지원하는 기능으로 EL의 함수로 지정하는 방식입니다.

1) JAVA 소스 코딩 : 정수 숫자를 "1, 100"과 같은 형식으로 변환해주는 기능을 제공하는 FormatUtil 클래스 작성
[source09\WEB-INF\scr\util\FormatUtil.java 소스 코딩]

EL에서 클래스의 메서드를 사용하기 위해서는 클래스의 메서드를 static으로 정의해야 하며,
static이 아닌 메서드는 사용할 수 없습니다.

2) 함수를 정의한 TLD(Tag Library Descriptor) 파일 작성
클래스 파일을 작성했다면 TLD 파일을 작성한다. TLD는 Tag Library Descriptor의 약자로서
이 파일은 태그 라이브러리에 대한 설정 정보를 담고 있습니다. 
TLD 파일은 WEB-INB\tlds 폴더나 WEB-INF\jsp 폴더와 같은 곳에 위치시켜서 활용합니다.
이번에는 WEB-INF\tlds 폴더에 TLD 파일을 위치시켰습니다.

[source09\WEB-INF\tlds\el-functions.tld 소스 코딩]

3) web.xml 파일에 TLD 내용 추가하기
TLD 파일을 작성한 다음에는 web.xml 파일에 TLD 파일 설정을 추가해야 합니다.
다음과 같이 위에서 제작한 TLD 파일에 대한 정보를 web.xml 파일에 추가해 줍니다.

[source09\WEB-INF\web.xml 소스 수정 코딩]

4) EL에서 함수 사용하기
함수를 정의한 태그 라이브러리를 사용할 준비가 되었으므로 EL에서 함수를 사용해봅니다.
EL에서 함수를 실행하려면 다음과 같은 형태의 코드를 사용합니다.
[다음]
<%@ taglib prefix=”pre” uri="..." %>
${pre:functionName(arg1, arg2, ..) }

taglib 디렉터브는 앞서 web.xml 파일에서 설정한 태그 라이브러리를 JSP 페이지에서
사용한다는 것을 명시합니다. taglib 디렉티브의 prefix 속성은 태그 라이브러리를
구분할때 사용할 접두어를 나타냅니다. EL에서 태그 라이브러리에 정의된 함수를 사용하려면
위 코드처럼 ${ 태그라이브러리접두어 : 함수이를（인자, 인자, ..）} 의 코드를 사용합니다.

[JSP 소스 코딩 : 앞서 작성한 el-functions.tld 파일은 함수 이름을 formatNumber로 지정했는데,
                    이 함수를 사용하는 JSP 소스 코드를 작성합니다]
[source09\viewNumber.jsp 소스 코딩]

EL에서 태그 라이브러리로 지정한 함수를 호출할 때 주의할 점은 실제 사용할 클래스의
메서드 이름이 아닌 TLD 파일의 〈name〉태그에서 지정한 이름을 사용한다는 점입니다.

5. EL에서 정적 메서드 호출하기 2
앞서 EL에서 클래스의 정적 메서드를 호출하기 위해 할 것이 많았습니다.
TLD 파일을 작성해야 하고, web.xml 파일도 설정해야 하고, taglib 디렉티브도 설정해야 합니다.
메서드를 호출할 때에도 TLD 파일에 설정한 이름을 사용해야 합니다.

EL 3.0 버전은 이런 복잡한 과정이 없이 정적 메서드를 호출할 수 있는 기능을 추가했습니다.
앞서 정적 메서드 호출 코드를 EL 3.0 기준으로 다시 작성하면 JSP 코드만 작성하면 됩니다.
즉, TLD 파일이나 web.xml 파일 설정을 할 필요가 없습니다.

* JSP 소스 코딩 : source09 폴더 안에 /viewNumber2.jsp 소스 코딩
JSP 2.3부터 page 디렉터브의 import 속성을 이용해서 임포트한 클래스의
정적 메서드를 EL에서 호출할 수 있습니다.
java.lang 패키지는 기본적으로 임포트 하므로 다음과 같이 Long, Integer와 같은
클래스의 정적 메서드도 사용할 수 있습니다.
${Long.parseLong('10')}

