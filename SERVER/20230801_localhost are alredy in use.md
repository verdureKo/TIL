# 포트번호 충돌 오류

Serveral ports(8005,8080) required by Tomcat v8.5 Server at localhost are alredy in use. The sever may already be running in another process, or a system process may be using the port To start this server you will need to stop the other process or change the port number(s).

```cmd
netstat -ano
```

해당 명령어는 모든 연결 포트와 수신 대기 포트를 알려주는 명령어이다.

```cmd
netstat -ano | findstr 8080
```

해당 명령어는 8080포트를 찾아서 8080포트만 표시된다.

```cmd
taskkill /f /pid (PID값)
```

![Alt text](/assets/포트충돌.png)
파란화살표는 포트번호 빨간화살표가 PID이다.

죽이고싶은 포트의 PID 입력 후 엔터를 누르면 된다.
