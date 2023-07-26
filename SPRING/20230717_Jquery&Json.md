# JSP jQuery와 JSON 사용

1. 동적 웹 프로젝트 생성 및 라이브러리 설치
 1) SIXTH_JSP 이름으로 동적 웹 프로젝트 생성 -
     프로젝트 클릭 선택 - Properties - Java Build Path - Libraries - Add Library
     - Server Runtime 에서 Apache Tomcat v9.0선택 추가

 2) SIXTH_JSP 프로젝트 클릭 - 우클릭 - Properties
    - Web Project Settings 에서 Context root: 입력란에 기존 "SIXTH_JSP"를 "/"로 변경해 주기 바랍니다.

 3) Tomcat 서버 Modules 설정에서 Path 설정을 기존 "/SIXTH_JSP"에서 "/" 변경 처리 후 저장합니다.

 4) WEB-INF 폴더에 있는 lib 폴더에 jstl-1.2.jar, json-simple-1.1.1.jar 파일을 넣어줍니다.

 5) 프로젝트 클릭 선택 - Properties - Java Build Path에서
    Web App Libraries 추가되어 있는지 확인 바랍니다.
    만약, Web App Libraries가 없다면
    프로젝트 클릭 선택 - Properties - Java Build Path - Libraries
     - Add Library - Web App Libraries 선택해서 추가해 주시기 바랍니다.

2. 소스 코딩 및 실행 확인

   1) WebContent 폴더에 image 폴더를 생성해 주고, 이미지들을 넣어줍니다.

   2) WebContent 폴더에 study01 폴더를 생성해 주고,
       jQuery1.html ~ jQuery5.html 파일들을 소스 코딩해서 실행 확인해 봅니다.

   3) WebContent 폴더에 study02 폴더를 생성해 주고,
      ajax1.html, ajax2.html 파일들을 소스 코딩해 줍니다.

   4) src 패키지에 sec01 - ajaxex 패키지를 만들어 주고,
      그 패키지 안에 AjaxTest1.java, AjaxTest2.java 파일들을 소스 코딩해 줍니다.

   5) WebContent 폴더에 study03 폴더를 생성해 주고,
       json1.jsp ~ json7.jsp 파일들을 소스 코딩해 줍니다.

   6) src 패키지에 sec02 - jsonex 패키지를 만들어 주고,
       그 패키지 안에 JsonServlet1.java, JsonServlet2.java, JsonServlet3.java 파일들을 소스 코딩해 줍니다.

   7) WebContent에 있는 study01, study02, study03에 있는
      JSP 파일들을 소스 코딩 후 각각 실행 확인을 해봅니다.