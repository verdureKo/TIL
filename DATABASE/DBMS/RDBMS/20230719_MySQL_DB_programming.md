# 데이터베이스 프로그래밍 : MySQL DB

1. 데이터베이스 기초 활용
1) 데이터베이스와 DBMS
우리가 흔히 '데이터베이스(Database)'라고 부르는 것의 주요 목적은 데이터를 저장했다가
필요할 때에 사용하는 것입니다. 데이터베이스를 관리하는 시스템을 DBMS(Database
Management System) 라고 부르며 주로 사용하는 DBMS로는 오라클, MySQL, MSSQL 서버 등이 있습니다.
데이터베이스는 데이터를 지속적으로 관리하고 보호하는 것을 주목적으로 하기 때문에,
DBMS는 데이터를 안정적으로 보관할 수 있는 다양한 기능을 제공하고 있습니다.

웹 어플리케이션을 구축할 때 주로 사용하는 데이터베이스는 관계형 데이터베이스
(Relational DBMS)입니다. 널리 사용하고 있는 오라클, MySQL, MS SQL 등은 모두
관계형 데이터베이스 입니다.

2) 테이블과 레코드
RDBMS에서 데이터를 저장하는 장소를 테이블(table)이라고 합니다.
테이블은 어떤 데이터를 저장하며 그 데이터의 길이는 최대 몇 글자인지 등의 정보를 갖고 있는데,
이처럼 테이블의 구조와 관련된 정보를 테이블 '스키마(Schema)'라고 부릅니다.
테이블의 구조는 각각의 정보를 저장하는 칼럼과 칼럼 타입 그리고 각 칼럼의 길이로 구성 됩니다.

3) 주요키(Primary Key)와 인덱스(Index)
테이블에 저장한 레코드를 사용하려면 각 레코드를 구별하는 방법이 필요합니다.
예를 들어, 전체 레코드 중에서 특정한 레코드를 한 개만 읽어 와야 한다고 해보면,
이때 각 레코드를 구분하는 방법이 존재하지 않으면 처음부터 끝까지
모든 레코드를 검색해야만 합니다. 레코드 수가 수십에서 수백 개라면
빠르게 찾을 수 있겠지만, 수십만에서 수백만 개라면 한 개의 레코드를 찾는 데 많은 시간이 걸립니다.
레코드를 미리 특정 값을 이용해서 정렬해 놓으면 좀 더 빠르게 레코드를 찾을 수 있을것입니다.
이런 목적으로 사용할 수 있는 것이 바로 주요키 (Primary key) 칼럼입니다.
주요키 칼럼은 하나의 테이블에 저장된 모든 레코드가 서로 다른 값을 갖는 칼럼을 의미합니다.
회원 아이디와 같이 서로 다른 값을 가져야 하는 칼럼을 주요키로 사용합니다.

주요키와 더불어 레코드를 분류할 때 사용되는 것이 인덱스(Index)입니다.
인덱스는 데이터의 순서를 미리 정렬해서 저장할 때 사용됩니다.
예를 들어, 도서관을 생각해보면, 도서관은 보통 책의 이름에 따라서 책의 위치를 정리해 놓습니다.
그렇게 함으로써 사람들이 책이름으로 쉽게 책의 위치를 찾을 수 있도록 하고 있습니다.
이와 비슷하게 데이터베이스도 레코드의 특정 칼럼을 사용해서 레코드를 쉽게 찾을 수 있도록
미리 정리된 표를 만들어 두는데, 이것이 바로 인덱스 입니다. 주요키도 인덱스의 일종으로서,
인덱스는 중복된 값에 대한 정렬이 가능하지만 주요키는 중복된 값을 가질 수 없다는 차이가 있습니다.

4) 데이터베이스 프로그래밍의 일반적 순서
데이터베이스를 사용하려면 DBMS 클라이언트에서 DMBS로 먼저 1) 데이터베이스에 연결해야 합니다.
그런 후에, DBMS 클라이언트에서 DBMS로 2) 데이터베이스에 데이터를 삽입하거나 변경하거나
삭제하는 등의 작업을 수행합니다. 그리고, DBMS로부터 DBMS 클라이언트로 3) 결과를 전송하고,
4) 마지막으로 원하는 작업을 수행했으면 연결을 종료 합니다.

위의 데이터베이스 프로그래밍의 네 단계 과정은
자바의 데이터베이스 프로그래밍인 JDBC 프로그래밍에서도 동일하게 적용됩니다.

5) 데이터베이스 프로그래밍의 필수 요소
데이터베이스 프로그래밍에는 다음과 같이 3개의 요소가 필요합니다.
• DBMS : 데이터베이스를 관리해주는 시스템
• 데이터베이스 : 데이터를 저장할 공간
• DBMS 클라이언트 : 데이터베이스를 사용하는 어플리케이션
DBMS는 앞에서 말했듯이 오라클이나 MySQL과 같은 데이터베이스 관리 프로그램을
의미합니다. DBMS가 필요하다는 말은 다시 말해서 오라클이나 MySQL 같은 프로그램을
설치해야 한다는 것을 뜻합니다.
데이터를 저장하려면 데이터를 저장할 공간인 데이터베이스를 만들어주어야 합니다.
데이터베이스를 생성하는 방법은 DBMS마다 다르므로, 실제로 사용할 DBMS에 맞게
생성해 주어야 합니다.
마지막으로 DBMS 클라이언트가 필요합니다. DBMS를 설치할 때 클라이언트가 함께
설치 되기도 하고, 클라이언트만 따로 설치할 수도 있습니다.
한 DBMS에는 여러 종류의 클라이언트가 존재하기도 합니다.
오라클은 SQL Plus라는 클라이언트를 함께 제공하며, TOAD라는 오라클 클라이언트 프로그램이 별도로 존재합니다.
MySQL을 설치할 때 사용되는 기본 클라이언트는 mysql.exe이지만,
MySQL Workbench라는 클라이언트를 따로 설치할 수도 있습니다.
자바에서는 JDBC Driver가 클라이언트의 역할을 대신하게 됩니다.

2. MySQL 데이터베이스 생성

1) MySQL 워크벤치를 실행하고 root 계정으로 DB에 연결합니다.
   그리고, 다음의 쿼리를 실행하여 데이터베이스를 생성합니다.

   create database chap17 default character set utf8;

[참고]
DBMS는 운영체제와 별도로 자신만의 사용자 계정을 갖고 있습니다.
MS-SQL의 경우는 윈도우즈 운영체제의 사용자 계정을 그대로 사용할 수도 있지만,
그 외 다른 DBMS는 별도의 사용자 계정을 관리하고 있습니다.
MySQL의 경우 root 계정이 기본적으로 제공되는 데이터베이스 관리 계정입니다.

데이터베이스를 추가한 뒤에는 MySQL에서 사용할 사용자를 추가합니다.
사용자를 추가하기 위해서는 다음과 같은 순서로 명령을 실행하면 됩니다.

create user 'jspexam'@'localhost' identified by 'jsppw';

grant all privileges on chap17.* to 'jspexam'@'localhost';

create user 'jspexam'@'%' identified by 'jsppw';

grant all privileges on chap17.* to 'jspexam'@'%';

CREATE USER 쿼리는 새로운 계정을 생성합니다. 구조는 다음과 같습니다.
create user '[계정]'@'[호스트]' identified by '[암호]'

[계정]은 DB 계정을 [암회] 연결할 때 사용할 암호를 입력입니다.
[호스트]는 해당 계정이 접근하는 호스트 정보를 입력 합니다.
호스트 값이 localhost인 경우 localhost에서 해당 계정으로 접근할 때
해당 암호를 사용한다는 것을 뜻합니다. 호스트 값이 '%'인 경우
모든 호스트에서 해당 계정으로 접근할 때 해당 암호를 사용한다는 것을 뜻합니다.
MySQL은 localliost와 다른 호스트를 구분하므로 사용자 계정을 생성할 때에는
localhost용 계정과 외부에서 접근할 때 사용할 계정을 각각 생성해주어야 합니다.

GRANT 쿼리는 MySQL DBMS 계정에 권한을 부여할 때 사용하는 명령어로서,
기본 구조는 다음과 같다.
grant [권한목록] on [데이터베이스].[대상] to '[계정]'@'[호스트]'

권한 목록이 all privileges이면 모든 권한을 부여합니다.
특정 권한만 부여하고 싶다면 다음과 같이 개별 권한 목록을 지정하면 된다.

grant select, insert, update, delete, create, drop on chap17.* to 'jspexam'@'%';

권한 부여 대상을 전체로 하고 싶다면 "*"을 값으로 사용합니다.
예를 들어, 다음 코드는 jspexam 계정에 대해 chap17 데이터베이스의
모든 테이블에 모든 권한을 부여합니다.

grant all privileges on chap17.* to 'jspexam'@'%';

GRANT 명령어를 사용해서 'jspexam' 계정이 chap17 데이터베이스를 사용할 수 있도록
권한을 부여했다면, 제대로 연결되는지 확인할 차례입니다.
MySQL 워크벤치에 다음 정보를 사용하는 연결을 새로 추가한 뒤 연결이 잘 되는지 확인해 봅니다.
• Connection Name : chap17 DB
• Username : jspexam
• Password : jsppw ([Store in Vault...] 버튼을 클릭해서 암호 입력)
• Default Schema : chap17

워크벤치의 연결 추가 대화창에 정보를 입력한 뒤 [Test Cormection] 버튼을 클릭해서,
연결에 성공하는지 확인 합니다.

3. SQL 기초
SQL은 'Structured Query Language'의 약자로서 데이터베이스로부터 데이터를 조회하고
삭제하는 등의 작업을 수행할 때 사용하는 언어입니다.

1) 주요 SQL 타입
자바에서 int, long, double, String과 같이 데이터 종류에 따라
알맞은 타입이 존재하는 것처럼 SQL도 저장할 데이터 종류에 따라
다양한 타입을 다음과 같이 제공합니다.
[다음] 표준 SQL의 주요 타입
   SQL 타입				의미
     CHAR	확정 길이의 문자열을 저장합니다. 표준의 경우 255글자까지만 저장할 수 있습니다.
  VARCHAR	가변 길이의 문자열을 저장합니다. 표준의 경우 255글자까지만 저장할 수 있습니다.
LONG VARCHAR	긴 가변 길이의 문자열을 저장합니다.
   NUMERIC	숫자를 저장합니다.
    DECIMAL	십진수를 저장합니다.
    INTEGER	정수를 저장합니다.
  TIMESTAMP	날짜와 시간을 저장합니다.
      TIME	시간을 저장합니다.
      DATE	날짜를 저장합니다.
      CLOB	대량의 문자열 데이터를 저장합니다.
(Character Large Object)
      BLOB	대량의 이진 데이터를 저장합니다.
(Byte Large Object)

[참고]
표준 SQL 타입이 존재하긴 하지만, DBMS는 표준 SQL 타입뿐만 아니라
DBMS 자체적으로 확장 타입을 추가 제공합니다.
예를 들어, 오라클은 VARCHAR2라는 타입을 제공하는데
이 타입은 4,000바이트까지 저장할 수 있습니다.
사실 오라클에서 VARCHAR와 VHARCAR2는 동일하므로 VARCHAR를 사용해도
4,000바이트까지 저장할 수 있습니다. MySQL도 비슷하게
Timestamp 타입뿐만 아니라 DATETIME이라는 타입을 제공하고 있습니다.
이렇듯 DBMS가 제공하는 확장 타입은 표준 SQL에 정의된 타입이 아니기 때문에
DBMS마다 서로 호환되지 않고 표준 SQL 타입과 다른 제약을 갖고 있습니다.
심지어 오라클의 VARCHAR처럼 표준 SQL과 이름은 같지만
완전히 다른 경우도 존재합니다. 따라서, DBMS가 제공하는 타입에 대해
기본적인 제약사항을 알고 타입을 사용해야 합니다.

2) 테이블 생성 쿼리
데이터가 실제로 저장되는 공간은 테이블이므로, 데이터베이스 프로그래밍을 하려면
테이블을 생성해야 합니다. 테이블을 생성할 때 사용하는 쿼리 형식은 다음과 같습니다.

[다음]
create table TABLENAME (
   COL_NAME1      COL_TYPE1(LEN1),
   COL_NAME2	COL_TYPE2(LEN2),
   ...
   COL_NAMEn      COL_TYPEn(LENn)
);
여기서 각 요소는 다음과 같습니다.
• TABLENAME : 테이블을 식별할 때 사용할 이름
• COL_NAME : 각 칼럼의 이름
• COL_TYPE : 각 칼럼에 저장될 값의 타입
• LEN : 저장될 값의 최대 길이

* 커멘드 CLI 확인 : SQL 쿼리를 MySQL콘솔 프로그램에서 직접 실행해 봅니다.
  아래의 Enter password: ***** 에서 *****에는 jsppw 를 입력하시기 바랍니다.

C:\Program Files\MySQL\MySQL Server 8.0\bin>mysql -u jspexam -p chap17 --default-character-set=utf8
Enter password: *****

* MySQL 워크벤치 입력 처리

create table MEMBER (
 MEMBERID VARCHAR(10) NOT NULL PRIMARY KEY,
 PASSWORD VARCHAR(10) NOT NULL,
 NAME VARCHAR(20) NOT NULL,
 EMAIL VARCHAR(80)
) engine=InnoDB default character set = utf8;

drop table MEMBER;

create table MEMBER (
 MEMBERID VARCHAR(10) NOT NULL PRIMARY KEY,
 PASSWORD VARCHAR(10) NOT NULL,
 NAME VARCHAR(20) NOT NULL,
 EMAIL VARCHAR(80)
)

위에서 engine=InnoDB는 MySQL에서 사용되는 구문입니다.
이 구문은 테이블을 InnoDB라는 저장 엔진을 사용해서 생성한다는 것을 의미합니다.
InnoDB 엔진을 사용하는 이유는 트랜잭션 때문인데,
InnoDB 엔진을 사용하지 않으면 트랜잭션이 올바르게 처리되지 않을 수 있습니다.

[참고]
위 테이블 생성 쿼리에서 "default character set = utf8"은
MySQL에서만 사용되는 구문으로 테이블에서 사용될 캐릭터 셋이
UTF-8임을 뜻합니다. 또한, 명령 프롬프트에서 mysql 프로그램을 실행할 때
--default-character-set 옵션의 값으로 utf8을 주었는데,
이는 mysql 클라이언트가 UTF-8 캐릭터 셋을 사용한다는 것을 의미합니다.
이 옵션을 주지 않고 쿼리를 실행하는 경우 UTF-8을 사용하는 테이블에 대한
글자 처리가 올바르게 되지 않습니다. 워크벤치를 사용하면 워크벤치가 캐릭터 셋 처리를
알아서 처리해주므로, mysql 프로그램보다 워크벤치를 사용하는 것이 편리합니다.

3) 데이터 삽입 쿼리
테이블에 데이터를 추가할 때는 INSERT 쿼리를 사용합니다.
INSERT 쿼리는 테이블에 한 레코드를 삽입할 때 사용하며 기본 문법은 다음과 같습니다.
[다음]
insert into [테이블이름] ([칼럼1], [칼럼2], [칼럼n])
values ([값1], [값2], ... [값n])

[테이블이름]은 레코드를 삽입할 테이블 이름을 나타냅니다. [칼럼]에는 값을 입력할
칼럼의 이름을 입력하고, [값]에는 해당 칼럼의 값을 입력합니다. 예를 들어,
앞서 생성한 MEMBER 테이블에 값을 추가하고 싶다면 아래와 같은 쿼리를 실행하면 됩니다.

insert into MEMBER (MEMBERID, PASSWORD, NAME)
values ('jangnara', '1234'，'장나라');

위 쿼리는 MEMBER 테이블의 MEMBERID, PASSWORD, NAME 킬럼의 값이 각각
'jangnara', '1234'，'장나라'인 레코드를 삽입 합니다. EMAIL 칼럼의 값은 지정하지
않았는데 이처럼 값을 지정하지 않으면 널(nuU) 값이 들어갑니다.

위 쿼리에서 큰따옴표가 아닌 작은따옴표를 사용하여 값을 표현하고 있는데,
SQL에서는 작은따옴표를 사용하여 문자열을 표시합니다.

[참고]
널(null) 값이란? 널 값은 칼럼에 어떤 값도 들어가 있지 않다는 것을 의미합니다.
예를 들어 , INTEGER 타입의 칼럼이 널 값을 가진 경우, 이 칼럼은 값을 갖고 있지 않은 상태가 됩니다.
즉, 0이나 1 등의 기본값을 사용하지 않고 아예 값이 없는 상태가 됩니다.
테이블 생성 쿼리에서 NOT NULL로 지정한 칼럼은 널을 값으로 갖지 못합니다.
칼럼 목록을 표시하지 않으면 전체 칼럼에 대해 값을 지정해야 합니다.
예를 들어, MEMBER 테이블에 레코드를 추가하려면 다음과 같이 칼럼명을 입력하지 않고
모든 칼럼의 값을 순서대로 지정해도 됩니다.

insert into MEMBER values ('kimheesun', '5678', '김희선', 'kimheesun@gmail.com')

=============================================================
* MySQL 워크벤치 쿼리문 적용 확인

insert into MEMBER (MEMBERID, PASSWORD, NAME)
values ('jangnara', '1234'，'장나라');

select * from member;

insert into MEMBER values ('kimheesun', '5678', '김희선', 'kimheesun@gmail.com')

select * from member;
=============================================================

[참고 : 값에 작은따옴표가 있을 때 처리 방법]
SQL에서는 작은따옴표를 사용해서 문자열을 표현합니다. 그래서, 값 자체에 작은따옴표가 포함되어
있으면 문제가 발생할 수 있습니다. 예를 들어. 다음의 SQL 쿼리를 살펴보면,
insert into MEMBER values('kimheesun', '5678', '김'희선', 'kimheesun@gmail.com)
세 번째에 삽입하는 값은 "김'희선' 인데, 실제로 쿼리는 '김' 부분만 값으로 인식하고 나머지 부분은
값으로 인식하지 않기 때문에 SQL 에러가 발생하게 됩니다. 값에 작은따옴표가 포함되어 있으면,
작은따옴표를 연달아 두 번 사용해서 작은따옴표를 표현해야 에러가 발생하지 않습니다.
예를 들어, "김'희선"이라는 문자열은 다음과 같이 표시합니다.
'김''희선'

4) 데이터 조회 쿼리
테이블에 저장된 데이터를 조회할 때에는 SELECT 쿼리를 사용합니다.
SELECT 쿼리의 기본 문법은 다음과 같습니다.
[다음]
select [칼럼1], [칼럼2], ...，[칼럼n] from [테이블이름]

여기서 [칼럼]은 읽어오고자 하는 칼럼의 목록입니다.
만약 전체 칼럼을 모두 읽고 싶으면 전체 칼럼 이름을 적는 대신
다음과 같이 별표('*')를 사용하면 됩니다.

select * from MEMBER;
select count(*) from MEMBER;

SELECT 쿼리는 기본적으로 모든 레코드의 목록을 읽어옵니다.
그런데 보통 특정 조건을 충족하는 레코드만 필요한 경우가 많기 때문에,
특정 조건을 충족하는 레코드만 조회하는 방법이 필요합니다.

=============================================================
* MySQL 워크벤치 쿼리문 적용 확인

select MEMBERID, NAME from MEMBER;

select * from member;
=============================================================

WHERE 절은 FROM 부분 뒤에 오며 다음과 같이 사용합니다.

select * from MEMBER where NAME = '장나라';

위 코드는 NAME 칼럼의 값이 '장나라'인 레코드의 목록만 읽어옵니다.
AND와 OR를 사용하면 한 개 이상의 조건을 동시에 부여할 수도 있습니다.

select * from MEMBER
select * from MEMBER where NAME = '장나라' and EMAIL = 'jangnara@gmail.com';

자바의 조건 연산자와 마찬가지로 AND를 사용하면 양쪽 조건을 모두 충족해야 하고
OR를 사용하면 두 조건 중의 하나만 충족하면 됩니다. 위 쿼리는 NAME 칼럼 값이
'장나라'이고 EMAIL 칼럼 값이 'jangnara@gmail.com'인 레코드만 검색합니다.

같지 않음을 표현할 때에는 '<>' 연산자를 사용합니다.
예를 들어, EMAL 칼럼의 값이 빈 문자열('')이 아닌 레코드를 검색하고 싶다면
다음과 같은 쿼리를 사용하면 됩니다.

select * from MEMBER where EMAIL <> "" ;

칼럼 값이 NULL이거나 NULL이 아닌 레코드를 구하고 싶다면 다음과 같이 NULL과
관련된 전용 쿼리를 사용할 수도 있습니다.

select * from MEMBER where EMAIL is NULL;
select * from MEMBER where EMAIL is not NULL;

'IS NULL' 연산자는 해당 칼럼이 NULL인지 여부를 판단하며,
'IS NOT NULL' 연산자는 해당 칼럼이 NULL이 아닌지 여부를 판단합니다.

그리고, 부등호 기호를 사용할 수도 있습니다. 예를 들어,
숫자 칼럼에서 값의 범위가 1부터 100 사이에 있는 레코드를 읽어오고 싶다고 한다면,
이 경우 다음과 같이 '<', '>', '<=', '>=' 등의 연산자를 사용하면 됩니다.
[참고] where SALARY >= 1000 and SALARY <= 200

아울러, LIKE 조건을 사용해서 특정 문장을 포함하고 있는지 검사할 수 있습니다. 예를 들어,
NAME 칼럼의 값이 '장'으로 시작하는 레코드를 찾고 싶다면 다음과 같이 LIKE 조건을
사용할 수 있습니다.
[참고] where NAME like '장%' -- '%'는 모든 것을 의미함

여기서 '%'는 모든 것을 의미하는 것으로서 위 조건은 NAME 칼럼의 값이 '장*****'의
형태를 갖는지 여부를 판단할 때 사용합니다. 만약 '%나%'과 같이 조건을 주면
앞뒤로 모든 문장이 오고 중간에 '나'가 포함된 값인지의 여부를 판단하게 됩니다.

[참고 : LIKE 검색시 주의 사항]
LIKE 검색은 편리하지만, 검색 속도가 매우 느립니다. 예를 들어 NAME 칼럼 값에 '은'이 포함된
레코드를 검색하고자 할 경우 다음과 같은 쿼리를 사용합니다.
   select... from member where name like '%은%'
레코드 수가 수천 개 이내라면 이 쿼리를 수행하는데 시간이 많이 걸리지 않지만
수백만이나 수천만 개라면 (포털의 회원수를 생각해 봅니다) 검색 속도가 참을 수 없을 만큼
느려집니다. 따라서. 빠른 검색 속도가 필요하다면 LIKE 검색 대신 별도의 검색 엔진을 사용해야 합니다.

5) 데이터 쿼리 조회(정렬)
게시판이나 회원 목록 등을 출력할 때 이름 순서나 아이디 오름차순 또는 번호 순으로
정렬하는 것이 보통입니다. SQL 쿼리에서는 ORDER BY 절을 사용해서 데이터 정렬을
처리 합니다. ORDER BY 절은 WHERE 절 뒤에 (WHERE 절이 없으면 FROM 절 뒤) 붙으며
다음과 같이 사용됩니다.
[다음]
 select ... from [테이블이름] where [조건절] order by [칼럼 1] asc, [칼럼2] desc, ...;

[칼럼]은 정렬하고 싶은 칼럼의 이름이고 칼럼 이름 뒤에 'asc'나 'desc’를 붙입니다.
'asc'를 붙이면 오름차순으로 정렬하고 'desc'를 붙이면 내림차순으로 정렬합니다.
여러 개의 칼럼을 사용하면 지정한 칼럼 순서대로 정렬합니다. 예를 들어, 다음의 쿼리를 살펴보면,
[다음 : MySQL 워크벤치 입력 확인]
select * from MEMBER order by NAME asc, MEMBERID asc；

위 쿼리문은 NAME 칼럼을 기준으로 오름차순으로 먼저 정렬하고, 그 상태에서
MEMBERID 칼럼에 대해서 오름차순으로 정렬하게 됩니다. 이때 주의할 점은
일단 NAME 칼럼으로 정렬된 상태가 되면, NAME 칼럼이 같은 값을 갖는 것들에 대해서만
MEMBERID 칼럼으로 정렬한다는 점입니다.

6) 데이터 쿼리 조회(집합)
집합 관련된 쿼리에는 sum(), max(), min(), count() 등의 함수가 있습니다. 이들 함수는
각각 총합, 최대, 최소, 개수를 구할 때 사용 됩니다. 예를 들어, 테이블의 SALARY 칼럼의
가장 큰 값과 가장 작은 값 그리고 전체 레코드의 칼럼 합을 구할 때는 다음과 같은 쿼리를 사용합니다.
[참고] select max(SALARY), min(SALARY), sum(SALARY) from ...;

전체 레코드 개수는 다음 쿼리를 사용해서 구할 수 있습니다.
select count(*) from MEMBER;

특정 조건에 해당하는 레코드에 대해서만 집합 관련 함수를 실행하고 싶다면
where 조건문을 붙이면 됩니다. 예를 들어, NAME 칼럼 값이 '장'으로 시작하는
레코드의 개수를 구하고 싶다면 다음과 같은 쿼리를 실행하면 됩니다.

select count(*) from MEMBER where NAME like '장%';

7) 데이터 수정 쿼리
데이터를 수정할 때에는 UPDATE 쿼리를 사용합니다. UPDATE 쿼리의 문법은 다음과 같습니다.
update [테이블이름] set [칼럼1] = [값1], [칼럼2] = [값2], ... where [조건절]; 

UPDATE 쿼리를 실행할 때 WHERE 절을 사용해서 조건을 명시하지 않으면
모든 레코드의 값을 변경합니다. 예를 들어, 다음 쿼리는 모든 레코드의 NAME 칼럼 값을
'장나라'로 변경 합니다.

update MEMBER set NAME = '장나라';

따라서, UPDATE 쿼리를 실행할 때에는 WHERE 절을 알맞게 사용해서 전체 레코드를
변경하지 않도록 주의해야 합니다.

=====================================================

[중요 : 위에 UPDATE 구문을 MySQL 워크벤치 활용 시 에러가 발생하면 다음과 같이 해결 바립니다]

select count(*) from MEMBER;

update MEMBER set NAME = '장나라' where EMAIL='madvirus@madvirus.net';

Error Code: 1175. You are using safe update mode and you tried to update a table without a WHERE that uses a KEY column To disable safe mode, toggle the option in Preferences -> SQL Editor and reconnect.

* 에러원인 : 테이블에서 키값을 이용한 update나 delete만을 허용하도록 되어 있는데, 그렇지 않게 좀더 넓은 범위의 sql을 적용하려고 할때 workbench에서 경고를 주는것입니다.
                즉 하나의 레코드만을 update, delete하도록 설정되어 있는데, 다수의 레코드를 update나 delete하는 sql명령어가 실행되기 때문에 발생을 하는 것입니다.
* 에러해결

  [해결방법1] Workbench Preferences에서 다음과 같이 안전모드(Safe mode)를 해제한다.

  Edit - Preferences - SQL Editor - (우측 스크롤 아래로) - Safe Updates(rejects UPDATEs and DELETEs with no restrictions) 체크 해제 - workbench 재시작(필수!)

  이렇게 하면 항상 Safe모드가 해제된 상태가 적용됩니다.

  [해결방법2 : 일시적인 Safe 모드 해제]

  아래와 같은 SQL 쿼리문으로 환경변수를 변경해 줍니다. (이렇게 하면 일시적인 Safe모드가 해제됩니다. 앞서 [해결방법1] 추천함)

   set sql_safe_updates=0;

=============================================================

update MEMBER set NAME = '장나라' where EMAIL='jangnara@naver.com';

select * from member;

=========================================================

8) 데이터 삭제 쿼리
DELETE 쿼리를 실행해서 레코드 단위로 데이터를 삭제할 수 있으며 문법은 다음과 같습니다.
delete from [테이블이름] where [조건절]
UPDATE 쿼리와 마찬가지로 DELETE 쿼리도 WHERE 절에 조건을 입력하지 않으면
전체 레코드를 삭제합니다. 즉, 다음 쿼리는 MEMBER 테이블에 있는 모든 레코드를 삭제합니다.

delete from MEMBER

따라서 특정 조건의 레코드를 삭제할 때에는 반드시 WHERE 절을 사용해서
삭제 범위를 지정해야 합니다. 예를 들어, 특정 회원 아이디에 대한 정보를 삭제하고 싶다면
다음과 같이 WHERE 절을 사용합니다.
[다음 : MySQL 워크벤치 활용 확인]

delete from member where memberid = 'jang';

select * from member;

insert into MEMBER values('jang', '5678', '장나라', 'jangnarna@nate.com')

select * from member;

=========================================================

9) 조인(Join)은 두 개 이상의 테이블에서 관련 있는 데이터를 함께 읽어올 때 사용됩니다.
조인의 기본 형식은 다음과 같습니다.
[다음]
select A.칼럼1, A.칼럼2, B.칼럼3, B.칼럼4
from [테이블1] as A, [테이블2] as B
where A.[칼럼x] = B.[칼럼 y]

위 쿼리에서 "[테이블 1] as A"는 테이블 1을 A로 표시한다는 것을 의미합니다.
마찬가지로 B는 [테이블2]를 나타냅니다. 위 쿼리는 테이블1의 칼럼x와 테이블2의
칼럼y의 값이 같은 레코드를 하나의 행(row)으로 읽어옵니다.

조인의 예를 들기 위해서 다음과 같은 테이블을 생성해 봅니다.

create table MEMBER_ETC (
	MEMBERID VARCHAR(10) NOT NULL PRIMARY KEY,
    BIRTHDAY CHAR(8)
);  -- Ctrl + Enter 클릭

insert into member_etc values('jang', '20220202')

insert into member_etc values('kimheesun', '20200203')

select * from member_etc;


MEMBER_ETC 테이블에 여러 레코드를 삽입한 후 다음과 같이 쿼리를 실행해 봅니다.

[다음 : MySQL 워크벤치 활용 확인]
select * from member as A, member_etc as B
where A.MEMBERID = B.MEMBERID;

위 쿼리는 두 테이블의 MEMBERID 칼럼이 같은 레코드를 함께 읽어오도록 하고 있습니다.
이때, 두 개 이상의 테이블로부터 같은 값을 갖는 칼럼을 사용하여 함께 레코드를 묶어서
읽어오는 것을 조인이라고 합니다. 조인을 사용하면 관련된 테이블로부터 필요한 칼럼을
모아서 한꺼번에 읽어올 수 있기때문에, 여러 테이블에 분산해서 저장된 정보를 읽어올 때
유용하게 사용할 수 있습니다.

[참고]
조인은 데이터베이스 프로그래밍에서 반드시 알고 있어야 하는 지식 중의 하나입니다.

