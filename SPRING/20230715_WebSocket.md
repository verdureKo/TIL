# WebSocket

1. Java Servlet 웹소켓 (WebSocket) 이해 및 활용

  보통의 웹 환경은 브라우저(클라이언트)에서 웹 서버에 Html 문서를 요청하면,

   웹 서버는 Html를 작성하고 브라우저(클라이언트)에 응답 한 후 연결을 끊는 비동기 소켓 통신입니다.

   Websocket는 브라우저(클라이언트)가 접속 요청을 하고 Web 서버가 응답 한 후 연결을 끊는 것이 아니고,

   Connection을 그대로 유지하고 브라우저(클라이언트)의 요청이 없어도 데이터를 전송할 수있는 프로토콜입니다.

   예를 들어, 채팅을 생각하면 사용자가 내용을 쓰고 서버에 전송합니다.

   즉, 브라우저(클라이언트)에서 서버로 데이터를 요청한 것입니다. 그리고 서버에서는 다른 응답 결과가 없으면

   그대로 응답 메시지를 보내지 않습니다.

   그러나 다른 사용자가 채팅 내용을 쓰고 서버로 전송하면 내 브라우저(클라이언트)로 메시지를 보내야 합니다.

   일반 웹 프로토콜의 경우는 서버와 브라우저(클라이언트)와 연결이 끊긴 상태이기 때문에

   브라우저에서 요청이 오지 않는 이상 다른 사용자의 메시지를 보낼 수 없습니다.

   WebSocket의 경우는 서버와 브라우저(클라이언트)가 끊기지 않은 상태이기 때문에

   브라우저(클라이언트)의 요청이 없어도 서버에서 브라우저로 메시지를 보낼 수가 있습니다.

   물론 웹 프로토콜의 경우, 몇 초당 갱신 주기를 만들어서 일정한 시간 단위로 요청을 하게 하여

   동기화를 할 수 있지만, 이 경우에는 트래픽이 많아서져서 웹 서버에 부담이 될 수 있습니다.(예시: socket.io)

   WebSocket의 경우는 HTML5부터 웹표준이 되었기에, 대부분의 웹브라우저에서 지원을 하고 있습니다.

   참고로, 프로토콜의 요청은 「ws://~」로 시작합니다. ssl 방식이라면 「wss://~」로 시작합니다.

   WebSocket을 구현하는 것은 크게 어렵지 않습니다. 별도로 소켓 서버를 구축하거나 프로토콜을

   선언하거나 해더를 관리하는 것도 없이 심플합니다.

  @OnOpen,@OnMessage,@OnClose,@OnError의 네가지 어노테이션으로 브라우저와
  
   통신 이벤트를 관리하는 것입니다.


2. Send to Server, Recieve From Server 웹소켓 프로그램 제작

 1) FIFTH_JSP 이름으로 동적 웹 프로젝트 생성 -
     프로젝트 클릭 선택 - Properties - Java Build Path - Libraries - Add Library
     - Server Runtime 에서 Apache Tomcat v9.0선택 추가

 2) FIFTH_JSP 프로젝트 클릭 - 우클릭 - Properties
    - Web Project Settings 에서 Context root: 입력란에 기존 "FIFTH_JSP"를 "/"로 변경해 주기 바랍니다.

 3) Tomcat 서버 Modules 설정에서 Path 설정을 기존 "/FIFTH_JSP"에서 "/" 변경 처리 후 저장함

 4) src 패키지 안에 websocket.java 파일 소스 코딩

  [중요 참고 : import javax.websocket.OnClose; 의 경우,
                 이클립스 좌측 Project Explorer 에서 - Libraries - Apache Tomcat v9.0
                 - 리스트 아랫부분에 websocket-api.jar 파일의 javax.websocket 패키지에 있는
                 OnClose 클래스를 보기 바랍니다]

3. 웹 소켓 접속을 위한 jsp파일 작성 코딩

   WebContent 폴더에 index.jsp 파일 소스 코딩
   [다음의 21행 소스에서 localhost:9001 부분에 본인의 PC 포트 번호 수정 적용해 줌]
   var webSocket = new WebSocket("ws://localhost:9001/websocket");

4. index.jsp 선택 - 마우스 우클릭 - Run As - Run On Server 톰켓 실행하고 웹 브라우저로 확인 바랍니다.

   1) 웹브라우저 화면 메시지 확인
      Server connect... 

   2) Console창 메시지 확인
       client is now connected... 

   3) Text 입력란에 jangnara 메시지 입력 후 Send 버튼 클릭

   4) 웹브라우저 화면 메시지 확인

       Send to Server => jangnara
       Recieve From Server => echo jangnara

   5) Console창 메시지 확인

       receive from client : jangnara
       send to client : echo jangnara

   6) Disconnect 버튼 클릭 후 웹브라우저 화면 메시지 확인

       Server Disconnect...
 
   7) Console창 메시지 확인

       client is now disconnected...    
 
[앞서 4번 참고]
1) WebSocket의 파라미터는 WebSocket의 접속 주소를 입력합니다. 프로토콜은 "ws://~"로 시작합니다.

   클라이언트 리스너 Javascript 내부 함수는 "onopen", "onmessgae", "onclose", "onerror"가 있습니다.

   onopen는 WebSocket 서버와 연결할 때 호출됩니다. onmessage는 서버에서 메시지를 수신하는 때 호출됩니다.

   onclose는 WebSocket 서버와 연결이 끊어 질 때 호출됩니다. onerror오류가 발생할 때 호출됩니다.

2) 웹브라우저 실행 연결이 되면 "Server connect ..."라는 메시지가 표시됩니다.

3) 송신 메시지를 작성하는 텍스트 박스에 "test websocket"을 입력하고 서버로 메시지를 보내면,

   서버에서 에코 메시지 답장도 옵니다. 마지막으로 WebSocket 접속 해제(Disconnec) 버튼을 클릭합니다.
 
   Console을 보면 전송 메시지가 보이고, Disconnect 버튼을 클릭하면 WebSocket의 접속 해제 로그가 나타납니다.

=========================================================================

5. Java에서 WebSocket의 Session 사용 방법(Broadcast)과 웹 채팅 소스 코딩을 해보겠습니다.

   소켓 통신 프로그램은 서버 소켓에서 클라이언트가 접속을 하게 되면 ClientSocket 인스턴스를 받습니다.

   그 ClientSocket 인스턴스로 연결을 유지(통신 동기화)하고 서버에서 클라이언트로 메시지를 보내게 됩니다.

    WebSocket에서는 Session의 객체가 있습니다. 이 Session의 객체는 브라우저로 부터 Socket 접속을 하면

    생성이 되고, 이 객체를 리스트등에 관리하면서 필요하면 꺼내서 메시지를 보낼 수도 있습니다.

    이 Session은 웹 Session(서버에 클라이언트 별 정보를 저장하는 오브젝트)과는 의미가 다릅니다.

    웹 세션은 브라우저가 Web Request를 할 때 마다,

    쿠키의 세션 키로 구분하여 유저의 정보를 가져오는 것을 말합니다.

    여기서 소켓 세션은 브라우저가 Websocket을 접속했을 때의 커넥션 정보가 있습니다.


6. 코딩 실습 3 : BroadSocket.java
   [정규표현식은 "중요_2) JAVA_정규표현식_Pattern_Matcher_활용.txt" 파일 참고 바람]

   앞서 WebSocket 리스너 구조와 비슷하지만, 이번에는 각 리스너에 Session 파라미터를 추가했습니다.

   Session 은 WebSocket의 커넥션 정보가 들어있는 인스턴스입니다.

   여기서 브라우저로 부터 메시지를 받으면 메시지 안에서 유저명을 추출하여

   다른 유저들에게 메시지를 보내는 형식으로 되어 있습니다.

   메시지의 형식은 「{{유저명}}메시지」의 형태로 되어있습니다.


7. 코딩 실습 4 : FIFTH_JSP 프로젝트 안에 WebContent 폴더 안에 index2.jsp 파일을 코딩 작성합니다.

     WebSocket서버에 메시지를 전송할 때의 메시지 형태는 「{{유저 명}}메시지」의 형태로 만들어서 보냅니다.
 
     그것은 서버의 handleMessage 함수에서 정규 표현식으로 유저명과 메시지 내용을 분리하는 것입니다.

     index.jsp 파일을 톰캣 서버로 실행하고, 실행한 후에 웹브라우저를 2개 실행하여 접속을 해봅니다.

     유저명은 각 "jangnara", "kimys"로 설정하여 메시지를 보냅니다.

     "jangnara"에서 보낸 메시지가 "kimys" 웹브라우저에도 보입니다.

      이렇게 간단하게 채팅 프로그램이 만들어 졌으며,

      서버 측의 콘솔(Console) 로그를 확인해 봅니다.

      클라이언트가 2개 접속해서 각각 메시지를 보낸 것을 확인할 수 있습니다.

    1) FIFTH_JSP 프로젝트 안에 WebContent 폴더 안에 index2.jsp 파일을 코딩 작성합니다.

    2) index2.jsp 선택 - 마우스 우클릭 - Run As - Run On Server 톰켓 실행하고 웹 브라우저로 확인 바랍니다.

       ① Eclipse 내장 웹브라우저(A) 화면 메시지 확인 : http://localhost:9001/index2.jsp

           anonymous     공란        Send     Disconnect

           Server connect...

       ② Console창 메시지 확인
           client is now connected... 

    3) 윈도우즈키 + R - Chrome 별도 새창 실행(B)  : http://localhost:9001/index2.jsp
       [anonymous 를 jangnara 로 수정함]
         jangnara       공란        Send          Disconnect

         Server connect...

    4) 윈도우즈키 + R - Chrome 별도 새창 실행(C)  : http://localhost:9001/index2.jsp
       [anonymous 를 kimys 로 수정함]
         kimys       공란        Send          Disconnect

         Server connect...

    5) 웹브라우저(A) anonymous 공란에 "안녕" 메시지 입력 후 Send 버튼 클릭

        [웹브라우저 메시지 확인]
        anonymous(me) => 안녕

        [Console창 메시지 확인]
        {{anonymous}}안녕

    6) 웹브라우저(B) jangnara 공란에 "응" 메시지 입력 후 Send 버튼 클릭    

        [웹브라우저 메시지 확인]
         anonymous => 안녕
         jangnara(me) => 응

        [Console창 메시지 확인]
        {{anonymous}}안녕
        {{jangnara}}응

    7) 웹브라우저(C) kimys 공란에 "반가워요~"메시지 입력 후 Send 버튼 클릭

        [웹브라우저 메시지 확인]      
         anonymous => 안녕
         jangnara => 응
         kimys(me) => 반가워요~
     
        [Console창 메시지 확인]
        {{anonymous}}안녕
        {{jangnara}}응
        {{kimys}}반가워요~

    8) 웹브라우저(A) anonymous Disconnect 버튼 클릭
        [웹브라우저 메시지 확인]      
        Server Disconnect...
        [Console창 메시지 확인]
        client is now disconnected...

   9) 웹브라우저(B) jangnara 와 웹브라우저(C) kimys 두명이서 메시지 주고 받기

  10_중요) 다른 PC 또는 스마트폰에서 접속하려면
            아래와 같이 index2.jsp 파일의 28행에서
   28행 :  var webSocket = new WebSocket("ws://localhost:9001/broadsocket");
            "ws://서버ip주소:9001/broadsocket" 형식으로 수정해 주시기 바랍니다.
    예시 : "ws://59.15.152.111:9001/broadsocket" 로 수정한 후에
   11)  다른 PC 또는 스마트폰에서 크롬 브라우저 실행 후  주소창에
          http://59.15.152.111:9001/index2.jsp 입력 후 실행 확인 바랍니다.
          참고로, 다른 PC 또는 스마트폰에서 접속이 안될 경우, 방화벽 체크도 하시기 바랍니다.

   12) 웹브라우저(B) jangnara Disconnect 버튼 클릭, 웹브라우저(C) kimys Disconnect 버튼 클릭
