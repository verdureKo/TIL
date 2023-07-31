# MVC패턴 게시판 CRUD 예제

## 클래스와 테이블 간의 연결 관계

![Alt text](/assets/image-4.jpg)

![Alt text](/assets/image-3.png)

1. 게시글 쓰기 기능은 다음과 같은 기능을 제공합니다.
1) 게시글을 쓰기 위한 폼은 제목과 내용을 제공합니다.
2) 폼에 제목을 입력하지 않았으면 다시 폼을 보여줍니다.
3) 로그인 한 사용자만 게시글 쓰기를 할 수 있습니다.
2. 위의 게시글 쓰기 기능 구현에 연관된 클래스의 구성은 다음과 같습니다.
1) ArticleDao 클래스와 ArticleContentDao 클래스 : article 테이블과 article_content 테이블에
데이터를 삽입하는 기능을 제공합니다.
2) WriteArticleService 클래스 : 새로운 게시글 쓰기 기능을 제공합니다.
두 DAO 클래스를 이용해서 기능을 구현합니다.
3) WriteRequest 클래스 : 신규 게시글을 등록할 때 필요한 데이터를 제공합니다.
4) WriteArticleHandler 클래스 : 사용자의 게시글 쓰기 요청을 처리합니다.
- GET요청이 오면 폼을보여주는 writeArticleForm.jsp를 뷰로 사용합니다.
- POST 요청이 오면 WriteArticleService를 이용해서 게시글 쓰기 기능을 실행합니다.
쓰기에 성공하면 writeArticleSuccess.jsp로 결과를 보여줍니다.
전송한 데이터가 유효하지 않으면 재입력을 위해 writeArticleForm.jsp로 다시 폼을 보여줍니다.
3. 로그인 한 사용자만 게시글 쓰기 기능을 사용할 수 있도록 제한하기 위해 LoginCheckFilter를 사용합니다.

![Alt text](image.png)

1. 게시글 목록 조회 기능은 다음과 같이 구현하였습니다.
1) 게시글 목록을 요청하면 10개 게시글의 번호, 제목, 작성자, 조회수를 표 형식으로 출력합니다.
2) 게시글 목록을 요청할 때 페이지 번호를 지정하지 않으면, 가장 최근에 작성한 게시글 10개를 최근 순으로 보여줍니다.
3) 요청한 페이지가 n이면, 가장 최근 게시글 순서로 (10*n)+1번째부터 10*(n+1) 번째까지 게시글 목록을 출력합니다.
예를 들어, 게시글 번호가 1부터 55번인 게시글 55개가 있다고 하면, 이 경우 55번 게시글이 가장 최근 게시글입니다.
이때 요청한 페이지가 3이면 화면에 표시할 게시글 번호 기준으로 35번 게시글부터 26번 게시글까지 10개 게시글을
출력합니다 (최신 기준으로 55~46번 글이 1페이지, 45~36번 글이 2페이지, 35~26번 글이 3페이지에 해당합니다)
4) 게시글 목록과 함께 이동 가능한 페이지 번호를 5페이지 단위로 표시합니다.
2. 게시글 목록을 표현하려면 다음의 두 데이터를 가져올 수 있어야 합니다.
1) 페이지 개수를 구하기 위한 전체 게시글 개수
2) 지정한 행 번호에 해당하는 게시글 목록
3) 위에 두 데이터를 가져오는데 필요한 메서드를 ArticleDao에 구현하였습니다.

![Alt text](image-1.png)

1. 게시글 조회 기능은 다음과 같이 구현하였습니다.
1) 요청한 번호에 해당하는 게시글의 내용을 출력합니다.
2) 게시글 조회수를 1증가 처리 합니다.
3) 존재하지 않는 게시글 번호를 요청하면 페이지 없음 상태 코드(404)를 응답합니다.
2. ArticleDao에서는 조회 관련 기능을 구현합니다.
게시글 조회 기능을 구현하려면 ArticleDao 클래스에 다음의 두 기능을 추가해야 합니다.
1) 특정 번호에 해당하는 게시글 데이터 읽기
2) 특정 번호에 해당하는 게시글 데이터의 조회수 증가하기

![Alt text](image-3.png)

1. 게시글 수정 기능은 다음과 같이 구현하였습니다.
1) 게시글 수정 폼은 게시글 제목과 내용을 표시합니다.
2) 게시글 수정은 작성자만 할 수 있습니다.
2. ArticleDao와 ArticleContentDao의 수정 관련 기능을 구현합니다.
1) ArticleDao의 update() 메서드는 파라미터로 전달받은 게시글 번호와 제목을 이용해서
데이터를 수정합니다. 이때, moddate 칼럼의 값을 현재시간으로 설정해서
데이터 최근 수정 시간을 기록합니다.
2) ArticleContentDao의 update() 메서드는 update 쿼리를 이용해서 content 칼럼의 값을 변경합니다

* 게시글 삭제 기능 구현 참고

1. 기능 구성
앞서, 제작한 게시판 프로그램에서 [게시글내용보기] 버튼 클릭 후 [글 삭제 진행] 버튼을
클릭하면, 게시글이 삭제되고, "게시글을 삭제했습니다." 메시지 보여준 후
[게시글목록보기] 버튼 클릭하면 게시글 목록을 보여주도록 기능을 구현합니다.

2. 코드구현

![Alt text](image-4.png)

1) DeleteArticleHandler : 사용자의 게시글 삭제 요청을 받습니다.
① deleteForm.jsp : 게시글 삭제 폼을 보여줍니다.
② deleteSuccess.jsp : 게시글 삭제완료가 성공한 폼을 보여줍니다.
2) DeleteArticleService : 게시글을 삭제하는 기능을 제공합니다.
명령어를 통해 테이블에서 삭제처리를 합니다.
3) DeleteRequest : 삭제할 데이터를 Request 처리합니다.
4) ArticleDao / ArticleContentDao : article 테이블과 article_content 테이블에
데이터를 삭제 처리하는 기능을 제공합니다.
5) board DB : board 데이터베이스를 제공합니다.

6. MySQL DB 워크벤치 실행해서 계정 생성 및 권한 부여, 테이블 생성

  1) 앞서 BOARD_SIGNUP에서 생성했던 jspexam계정(비밀번호 : jsppw)를 그대로 활용합니다.

     MySQL DB 워크벤치 - 왼쪽 상단 집모양 아이콘 클릭 - MySQL Connections 글자 옆 + 버튼 클릭
     - Connection Name: 란에 mysql_board 입력
     - Username: 란에 jspexam 입력
     - Password: 에서 Store in Vault... 버튼 클릭 - Password: 란에 jsppw 입력 - OK 버튼 클릭
     - Default Schema: 란에 board 입력 - 아래 Test Connection 클릭 - OK 버튼 클릭

  2) MySQL 워크벤치 : 데이터베이스 및 계정 정보 확인(앞서 BOARD_SIGNUP에 이어서 개발합니다)

	use board;

	select version();

	select user();

	show databases;

	show tables;

 3) MySQL 워크벤치 : article 테이블 2개 생성 쿼리

	create table board.article (
	    article_no int auto_increment primary key,
	    writer_id varchar(50) not null,
	    writer_name varchar(50) not null,
	    title varchar(255) not null,
	    regdate datetime not null,
	    moddate datetime not null,
	    read_cnt int
	) engine=InnoDB default character set = utf8;

	select * from board.article;

	create table board.article_content (
	    article_no int primary key,
	    content text
	) engine=InnoDB default character set = utf8;

	select * from board.article_content;

 4) MySQL 워크벤치 : article, article_content 입력 내용 확인

	select * from article;

	select * from article_content;

	show tables;
  
 7. 기능 확인

  1) BOARD_ARTICLE 프로젝트 클릭 선택 - 마우스 우클릭 - Run As - Run On Server
     (index.jsp 파일 클릭 - 마우스 우클릭 - Run As - Run On Server 해도 됨)
     (index_custum_tag_version.jsp 파일 클릭 - 마우스 우클릭
      - Run As - Run On Server 해도 됨. 이때, CT는 커스텀 태그 활용 나타냄)

  2) [회원가입하기] 클릭 - 아이디: 란에 예시(jangnara) 입력
      - 이름: 란에 예시(장나라) 입력
      - 암호: 란에 예시(12345) 입력
      - 확인: 란에 예시(12345) 입력
      - 가입신청 버튼 클릭
      - "장나라님, 회원 가입에 성공했습니다." 메시지 확인

  3) http://localhost:9001/login.do 로 이동해서
     - 아이디: 란에 예시(jangnara) 입력
     - 암호: 란에 12345 입력
     - 로그인 버튼 클릭
     - "CT: 장나라님, 안녕하세요. [로그아웃하기] [암호변경하기]" 확인(이때, CT는 커스텀태그 적용을 나타냄)

  4) 로그인 후 다음의 경로로 접근해 봄.
      [다음 : 아래의 경로로 접근해 봄]
      http://localhost:9001/article/write.do

    - 제목: 란에 예시(첫번째 글) 입력
    - 내용: 란에 예시(첫번째 글 내용) 입력
    - 새글 등록 버튼 클릭
    - 게시글 등록 성공 메시지 확인
      
    - [게시글목록보기] 버튼 클릭
    - 제목 아래 "첫번째 글" 클릭
    - [목록] 버튼 클릭 - 조회수 1 카운트 올라감 확인
    - 다시 제목 아래 "첫번째 글" 클릭
    - [게시글 수정] 버튼 클릭 
    - 제목: 란에 예시(첫번째 글 수정) 수정 입력
    - 내용: 란에 예시(첫번째 글 내용 수정) 수정 입력
    - 글수정 버튼 클릭
    - "게시글을 수정했습니다." 메시지 확인
    - [게시글목록보기] 클릭
    - 제목 수정된거 확인하고, 다시 제목 아래 "첫번째 글 수정" 클릭
    - 내용 수정된거 확인하고, [게시글삭제] 클릭
    - "선택하신 게시글을 삭제하시겠습니까?" 메시지 확인
    - [목록으로 돌아가기] 클릭
    - 다시 제목 아래 "첫번째 글 수정" 클릭
    - [게시글삭제] 클릭
    - "선택하신 게시글을 삭제하시겠습니까?" 메시지 확인
    - 글 삭제 진행 버튼 클릭
    - "게시글을 삭제했습니다." 메시지 확인
    - [게시글목록보기] 클릭하고, 게시글 삭제 확인
    - [게시글쓰기] 클릭
    - 제목: 란에 예시(두번째 글) 입력
    - 내용: 란에 예시(두번째 글 내용) 입력
    - 새글 등록 버튼 클릭
    - 게시글 등록 성공 메시지 확인
    - [게시글내용보기] 클릭하고 글 내용 확인
    - [목록] 버튼 클릭
      
  5) MySQL 워크벤치에서 다음의 쿼리문으로 데이터베이스 게시글 정보 확인

     select * from article;

     select * from article_content;

[참고 사항 : MySQL 시퀀스 초기화 방법 적용]
"중요) MySQL 시퀀스 초기화 방법 메모_무단 전재 및 배포 금지.txt" 내용도 함께 참고 바랍니다.

* MySQL 워크 벤치에서 다음의 쿼리문을 처리해 줍니다.

	delete from article;

	delete from article_content;

	ALTER TABLE article AUTO_INCREMENT=1;

	ALTER TABLE article AUTO_INCREMENT=1;
	       SET @COUNT = 0;
	       UPDATE article SET article_no = @COUNT:=@COUNT+1;

* 로그인 후 다음의 경로로 접근해서 게시글을 작성하고, [글목록보기] 클릭
  - 글목록 웹페이지에서 시퀀스 번호가 1로 초기화 되었는지 확인해 봅니다.
 [다음 : 아래의 경로로 접근해 봄]
  http://localhost:9001/article/write.do
