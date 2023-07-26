※ ServletContextListener 구현

서블릿은 다양한 시점에서 발생하는 이벤트와 이벤트를 처리하기 위한
인터페이스를 정의하고 있습니다. 이들 이벤트와 인터페이스를 이용하면
웹 어플리케이션에서 필요로 하는 데이터의 초기화나 요청 처리 등을 추적할 수 있게 됩니다.
서블릿 규약은 다양한 이벤트를 처리할 수 있는 인터페이스를 정의하고 있는데,
우리는 그 중에서 ServletContextListener 인터페이스의 활용 방법을 구현해 보겠습니다.

1. ServletContextListener를 이용한 이벤트 처리
웹 컨테이너는 웹 어플리케이션(컨텍스트)이 시작되거나 종료되는 시점에
특정 클래스의 메서드를 실행할 수 있는 기능을 제공하고 있습니다.
이 기능을 사용하면 웹 어플리케이션을 실행할 때 필요한 초기화 작업이나
웹 어플리케이션이 종료된 후 사용된 자원을 반환하는 등의 작업을 수행할 수 있습니다.

웹 어플리케이션이 시작되고 종료될 때 특정한 기능을 실행하려면
다음과 같이 코드를 작성하면 됩니다.
1) javax.servlet.ServletContextListener 인터페이스를 구현한 클래스를 작성합니다.
2) web.xml 파일에 위에 "1)"에서 작성한 클래스를 등록합니다.

javax. servlet. ServletContextListener 인터페이스는 웹 어플리케이션이
시작되거나 종료될 때 호출할 메서드를 정의한 인터페이스로서,
다음과 같은 두 개의 메서드를 정의하고 있습니다.
• public void contextInitialized(ServletContextEvent sce)
  웹 어플리케이션을 초기화할 때 호출합니다.
• public void contextDestroyed(ServletContextEvent sce)
  웹 어플리케이션을 종료할 때 호출합니다.

웹 어플리케이션이 시작되거나 종료될 때 ServletContextListener 인터페이스를
구현한 클래스를 실행하려면 web.xml 파일에 <listener>태그와 <listener-class>태그를
사용해서 완전한 클래스 이름을 명시해주면 됩니다.

=============================================================================

※  프로잭트 생성
1) [File] - [New] - [Dynamic Web Project] 메뉴를 실행합니다.
2) New Dynamic Web Project 대화창에서 다음과 같이 설정 후
   [Finish] 버튼을 클릭해서 프로젝트를 생성합니다.
   a. Project name : ServletContextListener_Basic
   b. Target runtime : Apache Tomcat v9.0 (톰켓 런타임을 다른 이름으로 등록했다면 해당 이름 사용)
   c. Dynamic web module version : 3.1
3) 프로젝트 생성 후 jstl-1.2.jar 파일을 WebContent/WEB-INF/lib 폴더에 복사합니다.

4) 프로젝트 클릭 선택 - Properties - Java Build Path - Libraries - Add Library
   - Server Runtime 에서 Apache Tomcat v9.0 선택 추가 바랍니다.

=============================================================================

우리는 앞서 DB 연동 예제에서 커넥션 풀을 초기화하기 위해 서블릿을 사용했는데,
이번에는 ServletContextListener를 이용해서 커넥션 풀을 초기화하는 클래스를
구현해보도록 합니다. 이 클래스는 다음과 같이 작성합니다.
[다음 :  커넥션 풀을 초기화하는 ServletContextListener 클래스 작성]
• web.xml 파일에 커넥션 풀을 초기화할 때 사용할 컨텍스트 초기화 파라미터를 설정합니다.
• ServletContextListener 인터페이스를 구현한 클래스는 contextlnitialized() 메서드에서
  컨텍스트 초기화 파라미터를 이용해서 커넥션 풀을 초기화하는 데 필요한 값을 로딩합니다.

* 1단계_중요) JAVA 소스 코딩 : src 패키지 안에 jdbc 패키지 생성 후, 앞서 DBCPInit.java 소스를 복사해 와서
                                DBCPInitListener.java 파일로 이름 변경하고 jdbc 패키지 안에 넣어줍니다.
                               그리고, 수정 코딩해 줍니다. 이때, poolConfig 컨텍스트 초기화 파라미터를
                               이용해서 커넥션 풀을 초기화하는 DBCPInitListener.java 소스 코딩을 합니다.
                               [중요 : DBCPInitListener.java 소스 안에 "수정(1) ~ 수정(17)"까지를 진행합니다]

* 2단계_중요) web.xml 소스 추가 코딩 : 커넥션 풀을 생성하는 데 필요한 컨텍스트 초기화 파라미터를
                                          다음과 같이 WebContent/WEB-INF/web.xml 파일에 설정합니다.
[다음 : (중요) WebContent/WEB-INF/web.xml 파일에 설정 소스]
(1안)
         ~~ 위에 생략 ~~
         <!-- web.xml 활용 ServletContextListener 설정 -->         
         <listener>
         	<listener-class>jdbc.DBCPInitListener</listener-class>
         </listener>
         <context-param>
	<param-name>poolConfig</param-name>
	<!-- 앞서 jdbcUrl의 DB주소에서 쌍다옴표 2개와 풀러스 사인 1개를 제거하고,
                  엔드 마크 3개를 엔드amp세미콜론으로 변경해서 소스 코드를 작성해 주시기 바랍니다. -->
	<param-value>
	jdbcdriver=com.mysql.cj.jdbc.Driver
	jdbcUrl = jdbc:mysql://localhost:3306/chap17?characterEncoding=UTF-8&amp;serverTimezone=UTC&amp;useSSL=false&amp;allowPublicKeyRetrieval=true
	dbUser = jspexam
	dbPass = jsppw
	poolName = chap17		
	</param-value>	
        </context-param>
          ~~ 아래 생략 ~~

(2안)
         ~~ 위에 생략 ~~
         <!-- web.xml 활용 ServletContextListener 설정 -->         
         <listener>
         	<listener-class>jdbc.DBCPInitListener</listener-class>
         </listener>
         <context-param>
	 <param-name>poolConfig</param-name>
	 <param-value>
	 jdbcdriver=com.mysql.cj.jdbc.Driver
	 jdbcUrl=jdbc:mysql://localhost:3306/chap17?characterEncoding=UTF-8&amp;serverTimezone=UTC
             dbUser=jspexam
	 dbPass=jsppw
	 poolName=chap17			
	</param-value>		
         </context-param>
          ~~ 아래 생략 ~~

* 3단계) JSP 소스 넣어줌 : 앞서 viewMemberUsingPool.jsp 파일을 WebContent 폴더 안에 복제해 넣어줍니다.
                                 이때, viewMemberUsingPool.jsp 파일은 수정하지 않고 그대로 사용해도 됩니다.
          [viewMemberUsingPool.jsp - 마우스 우클릭 - Run As - Run On Server 웹 브라우저 실행 확인합니다]

2. 애노테이션을 이용한 리스너 등록
서블릿 3.0 버전부터는 web.xml 파일에 등록하지 않고, @WebListener 애노테이션을 리스너 클래스에 적용하면
자동으로 리스너로 등록됩니다.

* 1단계) web.xml 소스 수정 코딩 : 앞서 web.xml 소스에서 리스너 등록 부분을 주석 처리 합니다(또는 삭제 처리합니다)

* 2단계) JAVA 소스 애노테이션 추가 코딩 : 앞서 DBCPInitListener.java 파일을 복제해서
           DBCPInitListenerAnnotation.java 파일로 이름 변경 후 다음과 같이 소스 코딩 추가해 줍니다.
  [다음]
   import javax.servlet.annotation.WebListener;

   // ServletContextListener를 애노테이션 방식으로 설정 시
   // web.xml 파일의 <listener> 태그를 주석 처리해 줘야 함.
   // 그리고, 아래와 같이 클래스 파일에 @WebListener 애노테이션 추가해 줘야 함
   @WebListener
   public class DBCPInitListener implements ServletContextListener {
   ...
   }

* 3단계) 앞서 viewMemberUsingPool.jsp - 마우스 우클릭 - Run As - Run On Server 웹 브라우저 실행 확인합니다.

viewMemberUsingPool.jsp
```
<%@page import="java.sql.SQLException"%>
<%@page import="java.sql.DriverManager"%>
<%@page import="java.sql.ResultSet"%>
<%@page import="java.sql.Statement"%>
<%@page import="java.sql.Connection"%>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>viewMemberUsingPool jsp 소스 코딩</title>
</head>
<body>
<!-- 커넥션 풀을 사용해서 member 리스트를 화면으로 출력 처리 함 -->

MEMBER 테이블의 내용
<table width="100%" border="1">
<tr>
	<td align="center">이름</td>
	<td align="center">아이디</td>
	<td align="center">이메일</td>
</tr>
<%
	Connection conn = null;
	Statement stmt = null;
	ResultSet rs = null;
	
	try{
		String jdbcDriver = "jdbc:apache:commons:dbcp:chap17";
		String query = "select * FROM member order by MEMBERID";
	
		// 2. 데이터베이스 커넥션 생성
		conn = DriverManager.getConnection(jdbcDriver);
		
		// 3. Statement 생성
		stmt = conn.createStatement();
		
		// 4. 쿼리 실행
		rs = stmt.executeQuery(query);
		
		// 5. 쿼리 실행 결과 출력
		while(rs.next()){
		%>	
		<tr align="center">
			<td><%= rs.getString("NAME") %> </td>
			<td><%= rs.getString("MEMBERID") %> </td>
			<td><%= rs.getString("EMAIL") %> </td>
		</tr>
		<%	
			}
		}catch(SQLException ex){
			out.println(ex.getMessage());
			ex.printStackTrace();		
		} finally{
		
			// 6. 사용한 Statement 종료
			if (rs != null) try{
				rs.close();
			} catch(SQLException ex){  }
			
			if (stmt != null) try{
				stmt.close();
			} catch(SQLException ex){  }
			
			// 7. 커넥션 종료
			if (conn != null) try{
				conn.close();
			} catch(SQLException ex){  }
	}
%>
</table>
</body>
</html>
```

web.xml
```
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://java.sun.com/xml/ns/javaee" xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd" id="WebApp_ID" version="3.0">

	<!-- @WebListener 애노테이션 이용한
	     ServletContextListener 설정 시
	          패키지와 클래스명이 jdbc.DBCPInitListenerAnnotation 같은때는
	          아래 형식의 listener 태그를 주석 처리해 주시기 바랍니다. -->

	<!-- web.xml 활용 ServletContextListener 설정 -->
	<listener>
		<listener-class>jdbc.DBCPInitListener</listener-class>		
	</listener>
	 
	<context-param>
		<param-name>poolConfig</param-name>
		<!-- 앞서 jdbcUrl의 DB주소에서 쌍다옴표 2개와 풀러스 사인 1개를 제거하고, 엔드 마크 3개를 엔드amp세미콜론으로 변경해서 소스 코드를 작성해 주시기 바랍니다. -->
		<param-value>
		jdbcdriver=com.mysql.cj.jdbc.Driver
		jdbcUrl = jdbc:mysql://localhost:3306/chap17?characterEncoding=UTF-8&amp;serverTimezone=UTC&amp;useSSL=false&amp;allowPublicKeyRetrieval=true
		dbUser = jspexam
		dbPass = jsppw
		poolName = chap17		
		</param-value>
	
	</context-param>

</web-app>
```
