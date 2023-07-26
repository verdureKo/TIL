# 서블릿 3 활용 JSP 파일 업로드 기능 활용

게시판이나 자료실，쇼핑몰 등에서는 문서 파일이나 이미지 파일을 등록하는 경우가
많습니다. 제품 이미지를 업로드한다든지, 대학교 내 게시판에 보고서를 업로드하는 등
웹 어플리케이션에서 업로드한 파일을 처리해야 경우가 있는데,
request 기본 객체가 제공하는 기능만으로는 업로드한 파일을 처리할 수가 없습니다.
파일 업로드 기능 구현은 다양한 방법으로 처리가 가능하며,
우리는 서블릿 3에서 제공하는 파일 업로드 기능을 사용해서
파일 업로드를 처리해 보려고 합니다.

1. 파일 전송 방식
일반 파라미터를 전송할 때 사용하는 인코딩과 파일을 업로드할 때 사용하는 인코딩은
다릅니다. 앞서 HTTP의 데이터 전송 방식은 크게 GET 방식과 POST 방식이 존재한다고
했는데 이 두 방식의 차이는 파라미터 데이터를 요청 URL로 전송하느냐 요청 몸체
데이터로 전송하느냐에 있습니다. 스트림 기반의 전송 방식인 POST 방식은
다시 다음의 두 가지 인코딩 방식에 따라 전송하는 데이터 형식이 달라집니다.

• application/x-www-form-urlencoded
• multipart/form-data

앞서 예시들은 application/x-www-form-urlencoded 인코딩을 사용해서 데이터를 전송했는데,
파일을 업로드하려면 multipart/form-data 인코딩을 사용해야만 합니다.
데이터를 multipart/form-data 인코딩 방식으로 전송하기 위해서는 다음과 같이
〈form〉태그의 enctype 속성값을 "multipart/form-data"로 지정해주면 됩니다.
그리고 "multipart/form" 인코딩 방식은 POST 전송 방식의 한 종류이므로 method 속성도
"post"로 지정해야 합니다.

웹 브라우저는 multipart/form-data 인코딩 방식의 데이터를 웹 서버에 전송할 때
application/x-www-form-urlencoded 방식과는 다른 형태로 전송합니다. 이 두 인코딩 방식의
차이를 살펴보기 위해서 다음과 같이 multipart/form-data 방식으로 데이터를 전송해주는
입력 폼을 생성해 봅니다.

* JSP 소스 코딩 : /WebContent/multipart_form.jsp

위의 multipart_form.jsp 실행 화면에서 [전송] 버튼을 클릭하면
multipart/form-data 인코딩을 이용해서 텍스트 데이터와 파일 데이터를
multipart_data.jsp로 전송 합니다. multipart_data.jsp는 전송받은 데이터를
그대로 응답 데이터로 출력해서 실제로 어떤 데이터가 전송되는지 확인할 수 있도록
다음과 같이 multipart_data.jsp 소스 코딩 후 실행 확인해 봅니다.

* JSP 소스 코딩 : /WebContent/multipart_data.jsp

2. 서불릿 3 파일 업로그 구현
서블릿 3.0에는 InputStream이나 외부 라이브러리를 사용하지 않고도
웹 브라우저가 업로드한 파일을 읽어올 수 있는 기능이 추가 되었습니다.
서블릿 3.0을 이용해서 파일 업로드를 처리하려면 다음의 두 가지만 하면 됩니다.
• HttpServletRequest의 getPart() 메서드를 이용해서 업로드 데이터 접근
• 서블릿이 multipart 데이터를 처리할 수 있도록 설정
  - @MultipartConfig 애노테이션을 사용하거나 또는
     web.xml에서 <multipart-config>태그 사용

1) Part를 이용한 업로드 데이터 접근
multipart/form-data 형식으로 전송된 데이터는 request.getParameter()와 같은
메서드로는 접근할 수 없으며, 서블릿 3.0에 새롭게 추가된 Part 인터페이스를
사용해서 접근해야 합니다. 접근하는 방식은 다음과 같습니다.
   ① HttpServletRequest.getContentType()을 이용해서 multipart/form-data인지 확인합니다.
   ② multipart/form-data인 경우
      A. HttpServletRequest의 getParts()나 getPart(name) 메서드를 이용해서 Part를 구합니다.
      B. Part의 Content-Disposition 헤더가 "filename="을 포함하면, 파일로 처리합니다.
      C. "filename="을포함하지 않으면 파라미터로 처리합니다.

* JAVA 소스 코딩 : "multipart/form-data"로 업로드된 데이터를 처리해주는
                        서블릿 코드를 작성해봄으로써 기본적인 사용법을 익혀보도록 합니다.
                        즉, 서블릿 3.1 의 Part를 이용해서 업로드 된 파일과
                        파라미터 값에 접근하는 JAVA 소스 코딩을 해봅니다.
                        [src/fileupload/UploadServlet.java]

HttpServletRequest는 다음의 두 가지 메서드를 이용해서 Part를 구할 수 있도록 하고 있습니다.
• Collection<Part> getParts() throws IOException, ServletException
• Part getPart(String name) throws IOException, ServletException
첫 번째 getParts() 메서드는 전체 Part 목록을 가져오고, getPart(name) 메서드는
해당 이름에 해당하는 Part를 가져옵니다. 예를 들어, request.getPart("title") 코드를
실행하면 HTML 폼에서 다음과 같이 이름이 "title"인 파라미터에 해당하는 Part를 리턴 합니다.

Part를 구한 뒤에는 Part가 제공하는 메서드를 이용해서 업로드 된 파일 정보나
파라미터 값을 구할 수 있습니다. Part가 제공하는 메서드는 다음과 같습니다.
• String getName() : 파라미터 이름을 구합니다.
• String getContentType() : 컨덴츠 타입을 구합니다.
• long getSize() : 업로드한 파일의 크기를 구합니다.
• String getSubmittedFileName() : 업로드한 파일의 이름을 구합니다.
• InputStream getInputStream() throws IOException : 데이터를 읽어올 수 있는
  InputStream을 구합니다. 파일이면 파일 데이터를 읽어오며,
  파일이 아닌 텍스트 파라미터이면 파라미터의 값을 읽어옵니다.
• void write(String filename) throws IOException : Part의 업로드 데이터를 filename이 지정한 파일에 복사합니다.
• void delete() throws IOException : Part 관련된 (임시로 생성된 파일 등) 파일을 삭제 합니다.
• String getHeader(String name) : 해당 Part에서 지정한 이름의 헤더 값을 구합니다.

2) 파일 업로드 처리를 위한 web.xml 파일 설정하기
서블릿이 파일 업로드를 처리할 수 있도록 하려면 추가적으로 서블릿에 Multipart와
관련된 설정을 추가해야 합니다. 설정을 추가하는 방법은 web.xml 파일로 설정하는 방법이 있고
애노테이션을 이용해서 설정하는 방법이 있는데, 먼저 web.xml 파일로 설정하는 방법을 살펴보도록 합니다.

web.xml 파일로 설정하는 방법은 간단합니다. 다음과 같이 <servlet> 설정에
<multipart-config>태그를 이용해서 관련 값을 지정해주기만 하면 됩니다.

* multipart 처리를 위한 web.xml 파일 서블릿 설정의 예시 소스 코딩
  [중요 : WebContent/WEB-INF/web.xml 소스 코딩]

3) @MultipartConfig 애노테이션을 이용한 설정
서블릿이 파일 업로드를 처리할 수 있도록 하는 또 다른 방법은
@MultipartConfig 애노테이션을 사용하는 것입니다.
@MultipartConfig 애노테이션은 다음과 같이 서블릿 클래스에 적용됩니다.

1단계_중요) 앞서 web.xml 파일의 multipart-config 태그 영역 주석 처리

2단계_중요) UploadServlet.java 파일에 @MultipartConfig 소스 추가 코딩

3단계_중요) 앞서 "2단계)" 소스 코딩 후 톰캣 재시작 - 실행 확인

즉, @MultipartConfig 애노테이션을 사용하면 web.xml 파일에
<multipart-config> 태그를 설정하지 않아도 서블릿이 Multipart 태그를 사용할 수 있게 됩니다.

@MultipartConfig에서 각 속성은 앞서 설명했던〈multipart-tag〉의 각 자식 태그와
동일합니다.

