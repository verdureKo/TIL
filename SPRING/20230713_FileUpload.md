# [JSP 파일 업로드 실습]

1. 파일 업로드 라이브러리 설치

  1) commons-fileupload-1.3.3.jar

  2) commons-io-2.6.jar

  3) jstl-1.2.jar

2. C드라이드에 file_repo 폴더 생성

3. Third_JSP 동적 웹프로젝트 생성 후 WebContent 폴더 안에
   test01 폴더 생성 후, 그 안에 uploadForm.jsp 파일 소스 코딩

4. Third_JSP 동적 웹프로젝트 src 패키지 안에
   ex01 패키지 생성 후, 그 안에 FileUpload.java 파일 소스 코딩

5. uploadForm.jsp - 마우스 우클릭 - Run on Server - 파일 업로드
  1) 파라미터1: 란에 test1 입력
  2) 파라미터2: 란에 test2 입력
  3) 파일1: 에서 파일 선택(예시 : flower_01.jpg)
  4) 파일2: 에서 파일 선택(예시 : flower_02.jpg)
  5) 업로드 클릭!

6. 파일 저장소(C:\file_repo)에 업로드된 파일 확인

7. 이클립스에서 Console 탭에 출력된
   "업로드 파일 정보와 매개변수 정보" 내용 확인

==============================================

[JSP 파일 다운로드 실습]

1. Third_JSP 동적 웹프로젝트 WebContent 패키지 안에
   test02 폴더 생성 후, 그 안에 first.jsp, result.jsp 파일 소스 코딩

2. Third_JSP 동적 웹프로젝트 src 패키지 안에
   ex02 패키지 생성 후, 그 안에 FileDownload.java 파일 소스 코딩

3. first.jsp - 마우스 우클릭 - Run on Server - 이미지 다운로드 버튼 클릭!

4. 업로드한 이미지가 브라우저에 출력되면 "파일 내려받기" 버튼 클릭하고,
   로컬 PC의 "다운로드" 폴더에 다운로드된 파일을 확인합니다.

5. 이클립스에서 Console 탭에 출력된 "다운로드 fileName 정보" 확인

==============================================