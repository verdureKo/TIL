# 팀 소개 웹 페이지 만들기_03

### **WIKI .** URI & URL?

- `URI` : 통합 자원 식별자(Identifier)
    - https://www.verdure.com/index.html    👉   URI (O), URL (O)
- `URL` : 웹 주소(Locator)
    - https://www.verdure.com/index     👉    URI (O), URL (X)

### **WIKI .** GET & POST ?

- `GET 요청`은, `url` 에 `?` 를 붙이고 `데이터`를 가져온다.
    - http://naver.com?param=value&param2=value2 
 - `POST 요청`은, `data` : `{}` 에 넣어서 `데이터`를 가져온다.
    - data: { param: 'value', param2: 'value2' },
    success: 성공하면, response 값에 서버의 결과 값을 담아서 함수를 실행한다.
