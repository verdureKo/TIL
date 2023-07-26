# 프로젝트 준비 및 데이터베이스 연동 프로그램 제작

4. 프로잭트 준비
1) [File] - [New] - [Dynamic Web Project] 메뉴를 실행합니다.
2) New Dynamic Web Project 대화창에서 다음과 같이 설정 후 [Finish] 버튼을 클릭해서
   프로젝트를 생성합니다.
   ① Project name : EIGHTH_JSP
   ② Target runtime : Apache Tomcat v9.0
   ③ Dynamic web module version : 3.1

5. JSP에서 JDBC 프로그래밍하기
자바에서 데이터베이스 프로그래밍을 할 때에는 JDBC API를 사용합니다.
JDBC는 Java DataBase Connectivity의 약자로서 자바에서 데이터베이스와
관련된 작업을 처리할 때 사용하는 API 입니다.
자바는 DBMS의 종류에 상관없이 하나의 JDBC API를 사용해서
데이터베이스 작업을 처리할 수 있기 때문에, 일단 익혀두면
모든 DBMS에 대해서 동일한 방식으로 데이터베이스 작업을 처리할 수 있게 됩니다.

1) JDBC의 구조
JSP를 포함한 자바 어플리케이션에서 데이터베이스를 사용할 때에는 데이터베이스
종류에 상관없이 JDBC API를 이용해서 데이터베이스에 접근합니다. 각각의 DBMS는
자신에게 알맞은 JDBC 드라이버를 제공하고 있습니다.
JDBC API는 JDBC 드라이버를 거쳐 데이터베이스와 통신을 합니다.
JDBC API를 사용하면 DBMS에 알맞은 JDBC 드라이버만 있으면
어떤 데이터베이스라도 사용할 수 있습니다. 현재 오라클，MySQL, MS-SQL 등
주요 DBMS에 알맞은 JDBC 드라이버를 제공하고 있기 때문에
JDBC 드라이버가 존재하지 않아서 JSP에서 데이터베이스 프로그래밍을 할 수 없는
상황은 발생하지 않을 것입니다.

2) JDBC 드라이버 준비하기
JDBC 프로그래밍을 하려면 DBMS에 알맞은 JDBC 드라이버를 준비해야 합니다.
JDBC 드라이버는 클래스 형태로 존재하며 일반적으로 Jar 파일로 제공됩니다.

=====================================================================

[중요 : JDBC 드라이버 준비하기]

1. JDBC 드라이버 다운로드 웹 사이트 접속

   https://dev.mysql.com/downloads/connector/j/5.1.html

2. zip 파일 다운로드

   mysql-connector-java-8.0.22.jar

3-1. 앞서 2번 zip 파일 압축 해제 후 다음의 파일을 이클립스 프로젝트 - WebContent/WEB-INF/lib 폴더에 넣어줌

   mysql-connector-java-8.0.22.jar

3-2. 이클립스 프로젝트 생성 - WebContent/WEB-INF/lib 폴더에 MySQL JDBC 드라이브 파일 복사,

     그러면, 이클립스 프로젝트가 사용하는 라이브러리에 복사한 jar 파일이 자동으로 포함되는 것을 확인 가능함

============================================================================


3) JDBC 프로그래밍의 코딩 스타일

JDBC 프로그램의 전형적인 실행 순서는 다음과 같습니다.
[다음]
1. JDBC 드라이버 로딩
2. 데이터베이스 커넥션 구함
3. 쿼리 실행을 위한 Statement 객체 생성
4. 쿼리 실행
5. 쿼리 실행 결과 사용
6. Statement 종료
7. 데이터베이스 커넥션 종료

"중요_그림_3) 커넥션 풀 기법_무단전재및배포금지.pdf" 파일을 참고 바랍니다.

위 순서에 맞춰서 테이블로부터 정보를 읽어와 출력하는 JSP 예제를 작성해 봅니다.

[중요]
JSP 소스 코딩 : EIGHTH_JSP/WebContent/viewMemberList.jsp

4) DBMS와의 통신을 위한 JDBC 드라이버
JDBC 드라이버는 DBMS와의 통신을 담당하는 자바 클래스로서
각 DBMS는 JDBC 드라이버를 jar 파일 형태로 제공합니다.

다음은 주요 데이터베이스의 JDBC 드라이버에 해당하는 클래스입니다.
• MySQL : com.mysql.jdbc.Driver
• 오라클 : oracle.jdbc.driver.OracleDriver
• MS SQL 서버 : com.microsoft.sqlserver.jdbc.SQLServerDriver

예를 들어, 오라클 JDBC 드라이버를 로딩할 때에는 다음과 같은 코드를 사용하면 됩니다.
try {
   Class.forName("oracle.jdbc.driver.OracleDriver");
} catch(ClassNotFoundException ex) {

[참고]
Class.forName() 메서드는 지정한 클래스 정보를 담고 있는
Class 인스턴스를 구해주는 기능만을 제공 합니다.
JDBC 드라이버에 해당하는 클래스들은 Class.forName() 메서드를 통해서
로딩될 때 자동으로 JDBC 드라이버로 등록합니다.

5) 데이터베이스 식별을 위한 JDBC URL
웹 주소를 구분할 때 http://www.google.com이나http://javacm.tistory.com과 같
은 URL을 사용하는 것처럼, 데이터베이스를 구분할 때에도 URL과 비슷한 형식을 갖는
JDBC URL을 사용합니다. 사용하는 JDBC 드라이버에 따라서 JDBC URL의 표현 방식에
차이가 나는데 일반적인 형식은 다음과 같습니다.
[다음]
jdbc:[DBMS]:[데이터베이스식 별자]

예를 들어，로컬 PC에서 실행 중인 MySQL 서버의 EIGHTH_JSP 데이터베이스를 나타낼 때
다음과 같은 JDBC URL을 사용하면 됩니다.
[다음]
jdbc:mysql://localhost:3306/EIGHTH_JSP

위에서 localhost는 MySQL 서버의 호스트 주소를 나타내며,
EIGHTH_JSP은 데이터베이스 이름을 나타냅니다.
3306은 MySQL 서버가 사용하는 포트 번호를 나타냅니다.

MySQL JDBC 드라이버가 MySQL 서버와 데이터를 주고받을 때 사용되는 캐릭터 셋을
올바르게 지정하지 않으면 한글이나 한자와 같은 글자가 잘못된 값으로 데이터베이스에
저장될 수 있습니다. 따라서, MySQL에서 한글 데이터를 올바르게 하기 위해서는
다음과 같이 추가 파라미터를 이용해서 캐릭터 셋을 알맞게 지정해주어야 합니다.
[다음]
jdbc:mysql://localhost:3306/EIGHTH_JSP?useUnicode=true&characterEncoding=utf8

UTF-8의 경우 MySQL에서는 utf8을 값으로 사용하며 EUC-KR은 euckr을 값으로
사용합니다. MySQL에서 지원하는 전체 캐릭터 셋 목록은 'show character set' 쿼리로
확인할 수 있습니다.

오라클에서 제공하는 JDBC 드라이버는 다음과 같은 형식의 JDBC UBL을 사용합니다.
jdbc:oracle:thin:@HOST:PORT:SID;
여기서, HOST, PORT는 각각 오라클이 설치된 호스트의 주소와 포트 번호를 나타내며,
SID는 사용할 데이터베이스의 SID를 나타 냅니다. 예를 들어, 로컬 서버에 설치된
오라클의 SID가 ORCL인 데이터베이스에 접근할 때에는 다음과 같은 JDBC URL을 사용합니다.
    jdbc:oracle:thin:@127.0.0.1:1521:ORCL

[참고]
오라클 드라이버에는 Thin 드라이버와 OCI 드라이버가 있습니다.
Thin 드라이버는 자바 언어로만 구현된 JDBC 드라이버로서 JDK만 설치되어 있으면
어디서든 사용할 수 있습니다. 반면에 OCI 드라이버는 네이티브(Native) 모듈을 사용하는
JDBC 드라이버로서 해당 모듈을 설치해주어야만 사용할 수 있습니다.
위에 오라클 JDBC URL을 보면 jdbc:oracle:thin과 같이 'thin'이 포함되어 있는데,
이는 Thin 드라이버를 사용해서 연결함을 뜻합니다.

6) 데이터베이스 커넥션
JDBC를 이용해서 데이터베이스를 사용하려면 데이터베이스와 연결된 커넥션을 구해야 합니다.
java.sql.Connection 타입이 데이터베이스 커넥션을 나타내며, java.sql.DriverManager 클래스가
제공하는 getConnection() 메서드를 사용해서 커넥션을 구할 수 있습니다.
DriverManager 클래스는 다음의 두 getConnection() 메서드를 제공하고 있습니다.
• DriverManager.getConnection(String jdbcURL)
• DriverManager.getConnection(String jdbcURL, String user, String password)

getConnection() 메서드의 jdbcURL은 데이터베이스에 연결할 때 사용할 JDBC URL을 나타냅니다.
user와 password는 데이터베이스의 계정과 암호를 나타냅니다.
JDBC URL, 올바른 DB 사용자 계정과 암호를 사용하면 DriverManager.getConnection() 메서드는
DB와 연결된 Connection 객체를 리턴 합니다. 이 Connection 객체를 사용해서 필요한 작업을 시작할 수 있습니다.

DriverManager.getConnection() 메서드는 Connection 객체를 생성하지 못하면
SQLException을 발생시킵니다. 따라서, getConnection() 메서드를 사용할 때에는
다음과 같이 try-catch 블록을 사용해서 SQLException에 대한 익셉션을 처리해야 합니다.

[다음]
Connection conn = null;
try{
   // 커넥션을 구하지 못하면 SQLException이 발생함
   conn = DriverManager.getConnection(...);
} catch(SQLException ex) {
  ... // 익셉션 처리
}

Connection 객체를 다 사용한 뒤에는 close() 메서드를 호출해서 Connection 객체가
사용한 시스템 자원을 반환해야 합니다. 그렇지 않으면 시스템 자원이 불필요하게
소모되어 커넥션을 구할 수 없는 상황이 발생할 수도 있습니다.

=================================================================


7) Statement 인터페이스(문자열 쿼리 실행 처리 인터페이스)를 사용한 쿼리 실행
Connection 객체를 생성한 후에는 Connection 객체로부터 Statement를 생성하고
쿼리를 실행할 수 있습니다. Statement는 다음과 같이 Connection의 createStatement()
메서드를 사용하여 생성합니다.

Statement stmt = conn.createStatement();

Statement 객체를 사용하면 쿼리를 실행할 수 있습니다.
쿼리를 실행할 때 사용하는 메서드는 다음과 같습니다.

• ResultSet executeQuery(String query) : SELECT 쿼리를 실행합니다.
• int executeUpdate(String query) : INSERT, UPDATE, DELETE 쿼리를 실행합니다.

executeQuery() 메서드는 SELECT 쿼리의 결과값을 java.sql.ResultSet 객체에
저장해서 리턴합니다. 두 번째 executeUpdate() 메서드는 INSERT, UPDATE, DELETE
쿼리를 실행하고, 그 결과로 변경된(또는 삽입된) 레코드의 개수를 리턴합니다.


* JSP 소스 코딩 : 아이디와 새로운 이름을 입력하면 MEMBER테이블의
                      NAME 칼럼 값을 변경하는 JSP 소스 코딩을 할것이며,
                      먼저, 아이디와 새로운 이름을 입력받는 폼을 출력해주는 JSP 소스 코딩을 합니다.
                      1단계) EIGHTH_JSP/WebContent/update/updateForm.jsp
                      2단계) EIGHTH_JSP/WebContent/update/update.jsp

8) ResultSet에서 값 읽어오기
Statement의 executeQuery() 메서드는 SELECT 쿼리를 실행할 때 사용되며,
SELECT 쿼리의 실행 결과를 java.sql.ResultSet 객체에 담아서 리턴 합니다.
따라서, ResultSet이 제공하는 메서드를 사용해서 결과값을 읽어올 수 있습니다.
ResultSet 클래스는 next() 메서드를 제공하는데, next() 메서드를 사용해서
SELECT 결과의 존재 여부를 확인할 수 있습니다.

[ResultSet클래스의 주요 데이터 읽기 메서드]
	메서드		           리턴 타입	   	  	  의미
getString(String name)	             String             지정한 칼럼 값을 String으로 읽어옵니다.
getString(int index)         		

getCharacterStream(String name)    java.io.Reader       지정한 칼럼 값을 스트림 형태로 읽어옵니다.
getCharacterStream(int index)                                 LONG VARCHAR 타입을 읽어올 때 사용합니다.
		
getlnt(String name)		    int	          지정한 칼럼 값을 int 타입으로 읽어옵니다.
getlnt(int index)			

getLong(String name)		   long	           지정한 칼럼 값을 long 타입으로 읽어옵니다.
getLong(int index)				

getDouble(String name)		   double  	지정한 칼럼 값을 double 타입으로 읽어옵니다.
getDouble(int index)	

getFloat(String name)		    float		지정한 칼럼 값을 float 타입으로 읽어옵니다.
getFloat(int index)		

getTimestamp(String name)          java.sql.Timestamp	지정한 칼럼 값을 Timestamp 타입으로 읽어옵니다. 
getTimestamp(int index)	                                    SQL TIMESTAMP 타입을 읽어올 때 사용합니다.

getDate(String name)                    java.sql.Date	지정한 칼럼 값을 Date 타입으로 읽어옵니다. 
getDate(int index)					SQL DATE 타입을 읽어올 때 사용합니다.

getTime(String name)                    java.sql.Time	지정한 칼럼 값을 Time 타입으로 읽어옵니다. 
getTime(int index)	                                                SQL TIME 타입을 읽어올 때 사용합니다.

ResultSet의 get 계열의 메서드는 현재 커서에서 데이터를 읽어옵니다.

ResultSet은 처음에 첫 번째 행 이전에 커서가 위치하기 때문에,
첫 번째 행에 저장된 데이터를 읽으려면 next() 메서드를 사용해서 커서를 이동시켜야 합니다.

"중요_그림_1) ResultSet_next 메서드와 커서의 이동.jpg" 이미지를 참고 바랍니다.

* JSP 소스 코딩 : 간단하게 파라미터로 아이디를 전달받으면 MEMBER 테이블로부터 해당 회원 정보를
                     읽어와 출력하는 JSP 소스 코딩을 해봅니다.
                     [EIGHTH_JSP/WebContenVviewMember.jsp]


9) ResetSet에서 LONG VARCHAR 타입 값 읽어오기
SQL의 LONG VARCHAR 타입은 대량의 텍스트 데이터를 저장할 때 사용합니다.
ResultSet에서 LONG VARCHAR 타입의 데이터를 읽어오려면 getCharacterStream() 메서드를
사용해야 합니다. ResultSet.getCharacterStream() 메서드는 리턴 타입이 java.io.Reader입니다.

* JSP 소스 코딩 : memberID 파라미터로 입력받은 값을 사용하여 정보를 검색해서 출력하는 JSP 소스 코딩
                     [EIGHTH_JSP/WebContent/viewMemberHistory.jsp]

10) PreparedStatement 인터페이스(SQL 구문을 미리 준비하고 활용하는 SQL 처리 인터페이스) 활용
java.sql.PreparedStatement는 java.sql.Statement와 동일한 기능을 제공합니다.
차이점이 있다면 PreparedStatement는 SQL 쿼리의 틀을 미리 생성해 놓고 값을 나중에
지정한다는 것입니다. PreparedStatement를 사용하는 순서는 다음과 같습니다.
① Connection.prepareStatement() 메서드를 사용하여 Preparedstatement 생성
② PreparedStatement의 set 메서드를 사용하여 필요한 값 지정
③ PreparedStatement의 executeQuery() 또는 executeUpdate() 메서드를 사용하여 쿼리를 실행함

PreparedStatement 객체를 생성한 다음에는 PreparedStatement가 제공하는 set 계열의
메서드를 사용해서 물음표를 대체할 값을 지정해주어야 합니다. 예를 들면 다음과 같이
각각의 물음표에 들어갈 값을 지정합니다.
pstmt.setString(1, "jangnara")； // 첫 번째 물음표의 값 지정
pstmt.setString(2, "장나라");	    // 두 번째 물음표의 값 지정
이때 첫 번째 물음표의 인덱스는 1이며, 이후 물음표의 인덱스는
나오는 순서대로 인덱스 값이 1씩 증가합니다. ResultSet의 get 계열의 메서드와
마찬가지로 PreparedStatement는 각각의 SQL 타입을 처리할 수 있는
set 계열의 메서드를 제공하고 있습니다. 이들 메서드는 다음과 같습니다.
[다음 : PreparedStatement 클래스가 제공하는 set 메서드]
          메서드                                        의미	
setString(int index, String x)	   지정한 인덱스의 파라미터 값을 X로 지정합니다.
setCharacterStream(int index,   지정한 인덱스의 파라미터 값을 LONG VARCHAR 타입의
Reader reader, int length)       값으로 지정할 때 사용합니다. Reader는 값을 읽어올 스트림이며,
                                        length는 지정한 문자열의 길이를 나타냅니다.
setlnt(int index, int x)	    지정한 인덱스의 파라미터 값을 int 값 x로 지정합니다.
setLong(int index, long x)	    지정한 인덱스의 파라미터 값을 long 값 x로 지정합니다.
setDouble(int index, double x)  지정한 인덱스의 파라미터 값을 double 값 x로 지정합니다.
setFloat(int index, float x)	    지정한 인덱스의 파라미터 값을 float 값 x로 지정합니다.
setTimestamp(int index,          지정한 인덱스의 값을 SQL TIMESTMAP 타입을 나타내는 
Timesetamp x)	                java.sql.Timestamp 타입으로 지정합니다.
setDate(int index, Date x)  	   지정한 인덱스의 값을 SQL DATE 타입을 나타내는 java.sql.Date 타입으로 지정합니다.
setTime(int index, Time x)	   지정한 인덱스의 값을 SQL TIME 타입을 나타내는 java.sql.Time 타입으로 지정합니다.

set 계열의 메서드를 사용하여 물음표에 해당하는 값들을 모두 지정했다면 다음의 두 메서드를 이용해서
쿼리를 실행할 수 있습니다. PreparedStatement를 생성할 때에 실행할 쿼리를 지정하기 때문에
이 메서드는 쿼리를 인자로 입력받지 않습니다.
• ResultSet executeQuery() : SELECT 쿼리를 실행할 때 사용하며 ResuItSet을 결과값으로 리턴합니다.
• int executeUpdate() : INSERT, UPDATE, DELETE 쿼리를 실행할 때 사용하며, 실행 결과로 변경된 레코드의 개수를 리턴합니다.

* JSP 소스 코딩 : 간단하게 PreparedStatement 클래스를 사용하여 MEMBER 테이블에 값을 삽입하는 JSP 소스 코딩을 해봅니다.
                     1단계) EIGHTH_JSP/WebContent/insert/insertForm.jsp
                     2단계) EIGHTH_JSP/WebContent/insert/insert.jsp

11) PreparedStatement 쿼리를 사용하는 이유
Statement 쿼리 대신 PreparedStatement 쿼리를 사용하는 주된 이유는 다음과 같습니다.
• 값 변환을 자동으로 하기 위해 사용합니다
• 간결한 코드 구현을 위해서 사용합니다.


6. 웹 어플리케이션 구동 시 JDBC 드라이버 로딩하기
웹 어플리케이션이 시작될 때 자동으로 JDBC 드라이버를 로딩하도록 만들려면
서블릿 클래스를 사용하면 됩니다. 이클립스 프로젝트를 사용하고 있다면
jdbc 패키지를 생성한 후에 jdbc 패키지에 MySQLDriverLoader 클래스를 추가한 뒤
코드를 작성하면 됩니다.

* JAVA 소스 코딩 : EIGHTH_JSP/src/jdbc/MySQLDriverLoader.java
  HttpServlet은 서블릿을 위한 상위 클래스입니다. 서블릿은 init() 메서드를 제공하고
  있는데, 이 init() 메서드는 서블릿을 초기화할 때 최초에 한 번 실행 됩니다.
  톰켓과 같은 컨테이너는 서블릿을 사용하기 전에 초기화를 수행하므로 init() 메서드에서
  JDBC 드라이버를 로딩하도록 구현하면 컨테이너를 실행할 때 JDBC 드라이버를 로딩할 수 있습니다.
  이클립스 프로젝트를 사용한다면 MySQLDriverLoader.java를 컴파일 할 필요가 없습니다.
   코드를 저장할 때 이클립스가 자동으로 컴파일해 주기 때문입니다.

MySQLDriverLoader.java를 작성했다면 웹 어플리케이션이 시작될 때 자동으로
MySQLDriverLoader 서블릿 클래스를 실행하도록 설정해야 합니다. 이를 위해
다음과 같이 web.xml 파일을 만들어서 <servlet> 태그를 추가해 줍니다.

[EIGHTH_JSP/WebContent/WEB-INF/web.xml 파일 소스 추가 코딩]

위와 같이 web.xml 파일에 〈servlet〉태그를 추가하면 웹 어플리케이션 구동 시
자동으로 MySQLDriverLoader 서블릿 클래스의 init() 메서드가 실행되므로,
결과적으로 웹 어플리케이션을 시작할 때 MySQL JDBC 드라이버를 로딩합니다.
[즉, MySQLDriverLoader 클래스의 init() 메서드에서 드라이버를 로딩합니다]
웹 어플리케이션을 시작할 때 MySQLDriverLoader 클래스를 이용해서
JDBC 드라이버를 로딩하므로 개별 JSP는 JDBC 드라이버를 로딩할 필요가 없어집니다.
(즉 JSP 코드에서 Class.forName() 코드를 사용할 필요가 없어집니다.
 다만,가끔 재로딩이 제대로 되지 않는 경우가 있는데 이럴 때는 서버를 재시작하면 됩니다)

7. JDBC 트랜잭션(일련의 처리 과정 수행을 의미함)

"중요_그림_2) DBMS 트랜잭션의 커밋과 롤백 처리.jpg" 이미지를 참고 바랍니다.

트랜잭션이 실제로 어떻게 동작하는지 살펴보기 위해 간단하게
세 개의 테이블에 데이터를 삽입하는 예제를 작성해보도록 합니다.
먼저 다음의 쿼리를 이용해서 두 개의 테이블을 생성해 봅니다.

[다음 : MySQL 워크벤치 이용 다음의 쿼리문을 처리해줌]

create table ITEM(
	ITEM_ID int not null primary key,
    NAME varchar(100)
) engine=InnoDB default character set = utf8;

select * from ITEM;

create table ITEM_DETAIL(
	ITEM_ID int not null primary key,
    DETAIL varchar(200)
) engine=InnoDB default character set = utf8;

select * from ITEM_DETAIL

* JSP 소스 코딩 : 위의 ITEM, ITEM_DETAIL  두 테이블에 데이터를 삽입하는 JSP 소스 코딩을 합니다.
                     [EIGHTH_JSP/WebContent/insertItem.jsp]

insertltem.jsp는 id 파라미터로 전달받은 값을 이용해서 ITEM 테이블과 ITEM_DETAIL 테이블에
삽입할 데이터를 생성 합니다. 첫 번째 쿼리 실행 후 error 파라미터 값이 null이 아니면
익셉션을 발생시켜서 두 번째 쿼리를 실행하지 않습니다. insertItem.jsp는
첫 번째 쿼리를 실행하기 전에 트랜잭션을 시작하기 때문에 error 파라미터가 존재할 경우
첫 번째 쿼리 실행 결과가 DB에 반영되지 않고 롤백 됩니다.
실제로 다음의 두 가지 URL을 요청해 봅니다.
• http://localhost:8080/EIGHTH_JSP/insertltem.jsp?id=1
• http://localhost:8080/EIGHTH_JSP/insertltem.jsp?id=2&error=t

위에서 http://localhost: 8080/chapl4/insertItem.jsp?id=1 URL을 실행하면
"데이터가 성공적으로 들어감" 이라는 결과 화면이 출력될 것입니다.
(이 URL을 두 번 실행하면 이미 동일한 값의 주요 키가 존재하기 때문에 주요키 중복 익셉션이 발생합니다)

DB에서 ITEM 테이블과 ITEM_DETAIL 테이블을 조회해 보면
주요키가 1인 데이터가 올바르게 삽입된 것을 확인할 수 있습니다.

[다음 select 쿼리문으로 확인해 봄]

select * from ITEM;

select * from ITEM_DETAIL

http://localhost:8080/EIGHTH_JSP/insertItem. jsp?id=2&error=t URL을 실행하면
error 파라미터가 존재하므로 첫 번째 쿼리 실행 후 익셉션을 발생시키고 트랜잭션이 롤백 처리 됩니다.
즉, http://localhost:8080/EIGHTH_JSP/insertItem. jsp?id=2&error=t URL 실행 후
ITEM 테이블과 ITEM_DETAIL 테이블을 보면 주요키가 2인 데이터가 ITEM 테이블과
ITEM_DETAIL 테이블에 모두 삽입되지 않은 것을 확인할 수 있을 것입니다.
즉, ITEM 테이블에 데이터를 삽입해주는 첫 번째 쿼리 실행 후 트랜잭션이 롤백된 경우,
쿼리 실행 결과가 DB에 반영되지 않는 것을 확인할 수 있습니다.

8. 커넥션 풀
지금까지 살펴본 예시들은 모두 데이터베이스 작업이 필요할 때 커넥션을 생성해서 사용했습니다.
이 방식을 사용하면 JSP 페이지를 실행할 때마다 커넥션을 생성하고 닫는 데 시간이 소모되기 때문에
동시 접속자가 많은 웹 사이트에서는 전체 성능이 낮아집니다. 성능 문제를 해결하기 위해서 사용하는
일반적인 방식은 커넥션 풀 기법을 사용하는 것입니다.

1) 커넥션 풀이란?
커넥션 풀 기법이란 데이터베이스와 연결된 커넥션을 미리 만들어서 풀(pool) 속에
저장해 두고 있다가 필요할 때에 커넥션을 풀에서 가져다 쓰고 다시 풀에 반환하는 기법을 의미합니다.

커넥션 풀 기법은 풀 속에 데이터베이스와 연결된 커넥션을 미리 생성해 놓습니다.
데이터베이스 커넥션이 필요하면, 커넥션을 새로 생성하는 것이 아니라 풀 속에 미리 생성된
커넥션을 가져다가 사용하고, 사용이 끝나면 커넥션을 풀에 반환 합니다.
풀에 반환된 커넥션은 다음에 다시 사용됩니다.

* 커넥션 풀의 특징은 다음과 같습니다.
[다음]
• 풀 속에 미리 커넥션이 생성되어 있기 때문에 커넥션을 생성하는데 드는 연결 시간을 줄일 수 있습니다.
• 커넥션을 계속해서 재사용하기 때문에 생성되는 커넥션 수가 일정하게 유지됩니다.

커넥션 풀을 사용하면 커넥션을 생성하고 닫는 데 필요한 시간이 소모되지 않기 때문에
그만큼 어플리케이션의 실행 속도가 빨라집니다. 또한, 한 번에 생성될 수 있는 커넥션 수를
제어하기 때문에 동시 접속자 수가 몰려도 웹 어플리케이션이 쉽게 다운되지 않습니다.

커넥션 풀을 사용하면 전체적인 웹 어플리케이션의 성능과 처리량이 향상되므로
많은 웹 어플리케이션이 커넥션 풀을 기본으로 사용하고 있습니다.

다양한 커넥션 풀 라이브러리가 존재하는데 우리는 오픈 소스 프로젝트인 DBCP API를 이용해서
커넥션 풀을 제공하는 방법을 살펴보도록 하겠습니다.

2) DBCP를 이용해서 커넥션 풀 사용하기
자카르타 프로젝트의 DB0P2 API를 사용할 때에는 다음과 같은 과정을 거치면 됩니다.
① DBCP 관련 jar 파일과 JDBC 드라이버 jar 파일 복사 및 설치하기
    commons-dbcp2-2.8.0.jar
    commons-logging-1.2.jar
    commons-pool2-2.9.0.jar

② 커넥션 풀 초기화 서블릿 클래스 제작
   1단계) JAVA 소스 코딩 : EIGHTH_JSP/src/jdbc/DBCPInit.java

   2단계) WEB-INF 폴더 안에 web.xml 파일 추가 소스 코딩

   3단계) 풀 이름은 PoolingDriver에 커넥션 풀을 등록할 때 지정합니다.
            이때, 풀의 이름으로 "EIGHTH_JSP"을 사용합니다.

③ 커넥션 풀로부터 커넥션 사용하기
    * JSP 소스 코딩 : 실제로 커넥션 풀을 사용하는 viewMemberUsingPool.jsp 파일을
                          커넥션 풀을 사용하도록 변경 처리함.

3) 커넥션 풀 속성 설명
앞에서 살펴본 DBCPInit 클래스를 보면 커넥션 풀을 설정할 때 GenericObjectPoolConfig 클래스를 사용했습니다.
이 클래스는 커넥션 풀의 크기, 커넥션의 검사 주기 등을 설정할 수 있는 메서드를 제공하고 있습니다.
예를 들어, 커넥션 풀의 최대 크기를 지정할 수 있는 setMaxTotal() 메서드를 제공 합니다.
setMaxTotal() 메서드를 포함해 커넥션 풀의 개수와 대기 시간을 설정하기 위한
GenericObjectPoolCbnfig 클래스의 설정 메서드는 다음과 같습니다.

[다음]
     메서드	                                의미                                                                 기본값
setMaxTotal(int)	풀이 관리하는 커넥션의 최대 개수를 설정합니다. 음수면 제한이 업습니다(Ex : -1)       8

* idle : 게으른, 대기하는, 유휴의
setMaxldle(int)	커넥션 풀이 보관할 수 있는 최대 유휴 개수를 지정합니다. 음수면 제한이 없습니다     8

setMinldle(int)	커넥션 풀이 유지할 최소 유휴 커넥션 개수를 지정합니다.                                    0
                        이 i 값이 maxldle 보다 크면 maxldle을 minldle 값으로 사용 합니다.                 

setBlockWhenExhausted(boolean) 풀이 관리하는 커넥션이 모두 사용중인 상태에서                           true
                                          커넥션을 요청할 때 풀에 커넥션이 반환될 때까지
                                          대기 할지 여부를 지정 합니다. true면 대기하고, 
                                          false면 NoSuchElementException 을 발생합니다.

setMaxWaitMillis(long)	blockWhenExhausted가 true일 때, 최대 대기 시간을 설정합니다.             -1L
                                    음수면 풀에서 커넥션을 구할 수 있을 때까지 대기 합니다.
                                    단위는 밀리초 입니다.	

커넥션 풀은 사용되지 않는 유휴 커넥션을 제거하는 기능을 제공합니다.
이 기능을 사용하면 주기적으로 커넥션을 검사하기 때문에,
DBMS에서 연결을 끊기 전에 먼저 커넥션을 풀에서 제거할 수 있습니다.

[GenericObjectPoolConfig 클래스의 유휴 커넥션 제거 및 검사 관련 설정 메서드]
	메서드	                                            의미                                                    기본값
setTimeBetweenEvictionRunsMillis(long) 풀에 있는 유휴 커넥션 검사 주기를 설정합니다.                    -1L
                                                  양수가 아니면 검사하지 않습니다. 단위는 밀리초입니다.	

setNumTestsPerEvictionRun(int)	각 주기 때마다 검사할 커넥션의 개수를 설정 합니다.                3
                                                음수면 유휴 커넥션 개수를 검사 개수의 절대값으로
                                                나눈 값을 사용 합니다.	

setMinEvictableldleTimeMillis(long)	풀에 머물 수 있는 최소 유휴 시간을 설정 합니다.             1800000L (30분)
                                                커넥션을 검사할 때 이 시간을 초과한 커넥션이
                                                제거 대상이 됩니다. 이 시간이 양수가 아니면
                                                유휴 시간으로 검사하지 않습니다. 단위는 밀리초입니다.	

setTestWhileIdle(boolean)	           true면 유휴 커넥션이 유효한지 검사합니다.                           false

setTestOnBorrow(boolean)	           true면 커넥션 풀에서 커넥션을 가져올 때 유효한지 검사합니다.   false

setTestOnReturn(boolean)	           true면 커넥션을 풀에 반환할 때 유효한지 검사합니다.	       false

커넥션 풀에 있는 커넥션 중 오랜 시간 동안 사용되지 않는 커넥션은 DBMS와 연결이
끊길 가능성이 높습니다. 연결이 끊긴 커넥션을 사용하면 프로그램 실행 도중 오류가
발생하기 때문에 주기적으로 커넥션 풀에 있는 커넥션을 검사해서 사전에 제거해주는 것이 좋습니다.
DBCP는 다음의 두 가지 기준으로 풀에 있는 커넥션을 검사합니다.
[다음]
① 커넥션이 최소 유휴 시간보다 오래 풀에 있는 경우(minEvictableldleTimeMillis)
② 커넥션이 유효한지 여부 확인 (testWhileldle)

위의 두 속성은 기본적으로 검사 주기(timeBetweenEvictionRmisMillis)가 양수일 때 적용 됩니다.
검사 주기가 양수가 아니면 유휴 커넥션 제거 처리 자체를 하지 않기 때문에,
검사 주기 값을 설정해야 유효 커넥션을 제거 합니다.

testWhileldle이 true면 PoolableConnectionFactory의 커넥션 검사 기능을 사용합니다.
앞서 DBCPInit을 보면 다음 코드를 찾을 수 있는데, 이 코드에서 setValidationQueiy() 메서드가
커넥션이 유효한지 검사할 때 사용할 쿼리를 다음과 같이 지정합니다.
[다음]
PoolableConnectionFactory poolableConnFactory =
        new PoolableConnectionFactory(connFactory, null)；
poolableConnFactory.setValidationQuery("select 1");

PoolableConnectionFactory 클래스의 커넥션 검사 기능과 관련된 설정 메서드는 다음과 같습니다.
[다음 : PoolableConnectionFactory의 커넥션 검사 기능과 관련된 설정 메서드]
  메서드                                               의미                                          기본값
setMaxConnLifetimeMillis(long)	커넥션의 최대 사용 시간을 설정합니다.           -1L
                                               커넥션을 생성한 뒤 최대 사용 시간이 지나면
                                               유효하지 않은 것으로 간주 합니다.
                                               양수가 아니면 적용하지 않습니다.
                                               단위는 밀리 초 입니다.	

setValidationQuery(String)	           커넥션을 검사할 때 사용할 쿼리를 설정 합니다.

GenericObjectPcx)lConfig 클래스에서 설정하는 풀의 몇 가지 속성은 성능에 큰 영항을
미치기 때문에 웹 어플리케이션의 사용량에 따라서 알맞게 지정해야 합니다.

• maxTotal : 사이트의 최대 커넥션 사용량을 기준으로 지정합니다. 이 값이 불필요하게
  커질 경우 커넥션 개수가 비대하게 늘어나 DBMS가 수용할 수 있는 수준을 넘어서면
  오히려 전체 성능에 좋지 않은 영향을 끼질 수 있습니다.

• minldle : 사용되지 않는 커넥션의 최소 개수를 0으로 지정하면 풀에 저장된
              커넥션 개수가 0이 될 수 있습니다. 이 경우 커넥션이 필요할 때
              다시 커넥션을 생성하게 됩니다. 따라서 커넥션의 최소 개수는
              시스템 사용이 가장 적은 시간을 기준으로 설정합니다.

• timeBetweenEvctionRunsMillis : 이 값을 설정해서 주기적으로 유휴 커넥션을 풀에서
  제거하는 것이 좋습니다. 커넥션의 동시 사용량은 보통 새벽에 최저이고 낮 시간대에 최대에
  이르게 됩니다. 이 두 시간대에 필요한 커넥션의 개수 차이는 수십에서 수백 개에 이릅니다.
  이때 최대 상태에 접어들었다가 최소 상태로 가게 되면 풀에서 사용되지 않는 커넥션의 개수가
  점차 증가합니다. 따라서 DB와의 연결이 끊기기 전에 유휴 커넥션을 미리 풀에서 제거해주는
  것이 좋습니다. 보통 10~30분 단위로 유휴 커넥션을 검사하도록 지정하는 것이 좋습니다.

• testWhileldle : 유휴 커넥션을 검사할 때 유효하지 않은 커넥션도 검사해서 연결이 끊긴
                     커넥션을 사전에 제거하는 것이 좋습니다.

• maxWaitMillis : 커넥션 풀에 커넥션이 없으면 일정 시간 대기 후 익솁선을 발생시키는
                     것이 좋습니다. 커넥션을 대기하느라 수십 초 이상 대기하면 사용자는
                     응답이 없으므로 브라우저의 새로 고침을 누르거나 DB를 사용하는 다른 페이지로
                     이동해서 다시 풀에서 가져오기 위해 대기하게 됩니다.
                     사용자가 아무 응답 없이 대기하는 것보다 1초 미만의 길지 않은 시간 안에
                     커넥션을 구하지 못하면 익셉션을 발생시켜서 알맞은 안내 화면을 보여주는 것이 좋습니다.

