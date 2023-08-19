# Java Email Sender 활용

![Alt text](/assets/mailsender-2.png)
![Alt text](/assets/mailsender-3.png)
![Alt text](/assets/mailsender-4.png)
![Alt text](/assets/mailsender-5.png)
![Alt text](/assets/mailsender-6.png)
![Alt text](/assets/mailsender-7.png)
![Alt text](/assets/mailsender-8.png)
![Alt text](/assets/mailsender-9.png)
![Alt text](/assets/mailsender-10.png)

1. 앱 비밀번호 생성: Gmail을 사용 중인 경우, 애플리케이션에 특정한 "앱 비밀번호"를 생성:
  a. Google 계정 설정으로 이동합니다 (<https://myaccount.google.com/>).
  b. "보안" 섹션에서 "Google에 로그인"을 찾고 "앱 비밀번호"를 클릭합니다.
  c. 앱을 선택하십시오 (이 경우 "메일" 또는 "기타 (사용자 정의 이름)"를 선택합니다).
  d. 화면 안내에 따라 앱 비밀번호를 생성합니다. 이 비밀번호는 일반 Google 계정 비밀번호 대신 애플리케이션에서 사용됩니다.

![Alt text](/assets/mailsender.png)
중괄호 안의 값을 발신자의 데이터로 변경하면 프로젝트에 메일센더를 연동할 수 있다.

2중 보안때문인지 클라이언트 시크릿을 넣어야 메일이 보내졌다.
아래 2, 3, 4번을 확인 후 구동하면 된다.

2. 구성 업데이트: Spring 애플리케이션에서 이메일 발송자 구성을 업데이트하여 새로 생성한 앱 비밀번호를 사용하도록 확인하세요.
3. SMTP 서버 및 포트 확인: Gmail의 SMTP 서버는 일반적으로 smtp.gmail.com이며 포트는 587 (또는 SSL의 경우 465)입니다.
4. 보안 연결: SMTP 서버에 연결할 때 사용하는 서버와 포트에 따라 TLS 또는 SSL을 사용하도록 연결 속성을 설정해야 할 수 있습니다.

"mail.smtp.port "은 SMTP서버와 통신하는 포트를 말하는데 앞서 진행한 gmail일 경우 587또는 465를 Naver의 경우 587을 사용한다.
