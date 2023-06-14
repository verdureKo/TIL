# HTTP 데이터를 객체로 처리하는 방법

## **@ModelAttribute**

### form 태그 POST

```url
POST http://localhost:8080/hello/request/form/model
```

- HTML의 form 태그를 사용하여 POST 방식으로 HTTP 요청을 보낼 수 있습니다.
- 이때 해당 데이터는 HTTP Body에 `name=Robbie&age=95` 형태로 담겨져서 서버로 전달됩니다.
- 해당 데이터를 Java의 객체 형태로 받는 방법은 @ModelAttribute 애너테이션을 사용한 후 Body 데이터를 `Star star` 받아올 객체를 선언합니다.

- Query String 방식

```url
GET http://localhost:8080/hello/request/form/param/model?name=Robbie&age=95
```

```java
// [Request sample]
// GET http://localhost:8080/hello/request/form/param/model?name=Robbie&age=95
@GetMapping("/form/param/model")
@ResponseBody
public String helloRequestParam(@ModelAttribute Star star) {
    return String.format("Hello, @ModelAttribute.<br> (name = %s, age = %d) ", star.name, star.age);
}
```

- **[코드 스니펫] helloRequestParam**

```java
// [Request sample]
// GET http://localhost:8080/hello/request/form/param/model?name=Robbie&age=95
@GetMapping("/form/param/model")
@ResponseBody
public String helloRequestParam(@ModelAttribute Star star) {
    return String.format("Hello, @ModelAttribute.<br> (name = %s, age = %d) ", star.name, star.age);
}
```

- `?name=Robbie&age=95` 처럼 데이터가 두 개만 있다면 괜찮지만 여러 개 있다면 @RequestParam 애너테이션으로 하나 씩 받아오기 힘들 수 있습니다.
- 이때 @ModelAttribute 애너테이션을 사용하면 Java의 객체로 데이터를 받아올 수 있습니다.
- 파라미터에 선언한 `Star` 객체가 생성되고, 오버로딩된 생성자 혹은 Setter 메서드를 통해 요청된 `name & age` 의 값이 담겨집니다.

⚠️ @ModelAttribute는 생략이 가능합니다.
이때, 생각해볼 문제가있습니다!
Spring에서는 @ModelAttribute뿐만 아니라 @RequestParam도 생략이 가능합니다.
그렇다면 Spring은 이를 어떻게 구분할까요?
간단하게 설명하자면 Spring은 해당 파라미터(매개변수)가 SimpleValueType이라면 @RequestParam으로 간주하고 아니라면 @ModelAttribute가 생략되어있다 판단합니다.
    SimpleValueType은 원시타입(int), Wrapper타입(Integer), Date등의 타입을 의미합니다.

## **@RequestBody**

- HTTP Body에 JSON 데이터를 담아 서버에 전달할 때 해당 Body 데이터를 Java의 객체로 전달 받을 수 있습니다.
- Body JSON 데이터

```url
POST http://localhost:8080/hello/request/form/json
```

```java
// [Request sample]
// POST http://localhost:8080/hello/request/form/json
// Header
//  Content type: application/json
// Body
//  {"name":"Robbie","age":"95"}
@PostMapping("/form/json")
@ResponseBody
public String helloPostRequestJson(@RequestBody Star star) {
    return String.format("Hello, @RequestBody.<br> (name = %s, age = %d) ", star.name, star.age);
}
```

```java
// [Request sample]
// POST http://localhost:8080/hello/request/form/json
// Header
//  Content type: application/json
// Body
//  {"name":"Robbie","age":"95"}
@PostMapping("/form/json")
@ResponseBody
public String helloPostRequestJson(@RequestBody Star star) {
    return String.format("Hello, @RequestBody.<br> (name = %s, age = %d) ", star.name, star.age);
}
```

- HTTP Body에 `{"name":"Robbie","age":"95"}`  `JSON` 형태로 데이터가 서버에 전달되었을 때 @RequestBody 애너테이션을 사용해 데이터를 객체 형태로 받을 수 있습니다.

⚠️ 데이터를 Java의 객체로 받아올 때 주의할 점이 있습니다.

- 해당 객체의 필드에 데이터를 넣어주기 위해 set or get 메서드 또는 오버로딩된 생성자가 필요합니다.
- 예를 들어 @ModelAttribute 사용하여 데이터를 받아올 때 해당 객체에 set 메서드 혹은 오버로딩된 생성자가 없다면 받아온 데이터를 해당 객체의 필드에 담을 수 없습니다.
- 이처럼 객체로 데이터를 받아올 때 데이터가 제대로 들어오지 않는다면 우선 해당 객체의 set or get 메서드 또는 오버로딩된 생성자의 유무를 확인하시면 좋습니다.

```java
package com.sparta.springmvc.request;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.*;

@Controller
@RequestMapping("/hello/request")
public class RequestController {
    @GetMapping("/form/html")
    public String helloForm() {
        return "hello-request-form";
    }

    // [Request sample]
    // GET http://localhost:8080/hello/request/star/Robbie/age/95
    @GetMapping("/star/{name}/age/{age}")
    @ResponseBody
    public String helloRequestPath(@PathVariable String name, @PathVariable int age)
    {
        return String.format("Hello, @PathVariable.<br> name = %s, age = %d", name, age);
    }

    // [Request sample]
    // GET http://localhost:8080/hello/request/form/param?name=Robbie&age=95
    @GetMapping("/form/param")
    @ResponseBody
    public String helloGetRequestParam(@RequestParam(required = false) String name, int age) {
        return String.format("Hello, @RequestParam.<br> name = %s, age = %d", name, age);
    }

    // [Request sample]
    // POST http://localhost:8080/hello/request/form/param
    // Header
    //  Content type: application/x-www-form-urlencoded
    // Body
    //  name=Robbie&age=95
    @PostMapping("/form/param")
    @ResponseBody
    public String helloPostRequestParam(@RequestParam String name, @RequestParam int age) {
        return String.format("Hello, @RequestParam.<br> name = %s, age = %d", name, age);
    }

    // [Request sample]
    // POST http://localhost:8080/hello/request/form/model
    // Header
    //  Content type: application/x-www-form-urlencoded
    // Body
    //  name=Robbie&age=95
    @PostMapping("/form/model")
    @ResponseBody
    public String helloRequestBodyForm(@ModelAttribute Star star) {
        return String.format("Hello, @ModelAttribute.<br> (name = %s, age = %d) ", star.name, star.age);
    }

    // [Request sample]
    // GET http://localhost:8080/hello/request/form/param/model?name=Robbie&age=95
    @GetMapping("/form/param/model")
    @ResponseBody
    public String helloRequestParam(@ModelAttribute Star star) {
        return String.format("Hello, @ModelAttribute.<br> (name = %s, age = %d) ", star.name, star.age);
    }

    // [Request sample]
    // POST http://localhost:8080/hello/request/form/json
    // Header
    //  Content type: application/json
    // Body
    //  {"name":"Robbie","age":"95"}
    @PostMapping("/form/json")
    @ResponseBody
    public String helloPostRequestJson(@RequestBody Star star) {
        return String.format("Hello, @RequestBody.<br> (name = %s, age = %d) ", star.name, star.age);
    }
}
```
