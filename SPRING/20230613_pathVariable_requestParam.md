# @PathVariable과 @RequestParam

## **Path Variable**

```url
GET http://localhost:8080/hello/request/star/Robbie/age/95
```

- Client 즉, 브라우저에서 서버로 HTTP 요청을 보낼 때 데이터를 함께 보낼 수 있습니다.
- 서버에서는 이 데이터를 받아서 사용해야하는데 데이터를 보내는 방식이 여러 가지가 있습니다.

- 데이터를 받기 위해서는 `/star/{name}/age/{age}`  이처럼 URL 경로에서 데이터를 받고자 하는 위치의 경로에 {data} 중괄호를 사용합니다.
- `(@PathVariable String name, @PathVariable int age)`
  - 그리고 해당 요청 메서드 파라미터에 @PathVariable 애너테이션과 함께 {name} 중괄호에 선언한 변수명과 변수타입을 선언하면 해당 경로의 데이터를 받아올 수 있습니다.

## **Request Param**

```url
GET http://localhost:8080/hello/request/form/param?name=Robbie&age=95
```

- 서버에 보내려는 데이터를 URL 경로 마지막에 `?` 와 `&` 를 사용하여 추가할 수 있습니다.
- ?name=Robbie&age=95
  - ‘Robbie’와 ‘95’ 데이터를 서버에 보내기 위해 URL 경로 마지막에 추가했습니다.

- @RequestParam은 생략이 가능합니다.
- `@RequestParam(required = false)`
  - 이렇게 required 옵션을 false로 설정하면 Client에서 전달받은 값들에서 해당 값이 포함되어있지 않아도 오류가 발생하지 않습니다.
  - `@PathVariable(required = false)` 도 해당 옵션이 존재합니다.
  - Client로 부터 값을 전달 받지 못한 해당 변수는 null로 초기화됩니다.

## **PostMan**

Postman은 HTML화면 없이도 응답값을 확인할 수 있다.
Postman은 API 수명 주기의 각 단계를 단순화하고 협업을 간소화하여 더 나은 API를 더 빠르게 생성할 수 있도록 한다.

[postman.com](https://www.postman.com/home)

- GET 요청: 전체조회 ![Get테스트](/assets/get.PNG)
- GET 요청: 선택조회 ![Get테스트](/assets/%EC%84%A0%ED%83%9D%EC%A1%B0%ED%9A%8C.PNG)
- POST 요청: 글쓰기 ![Get테스트](/assets/post2.PNG)
- PUT 요청: 선택수정 ![Get테스트](/assets/put.PNG)
- DELETE 요청: 선택삭제 ![Get테스트](/assets/deletee.PNG)

뒤늦게 사용법을 제대로 알긴했지만 너무나 신빡하다.
