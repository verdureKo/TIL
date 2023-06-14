# 동적 페이지와 정적 페이지 처리

## 동적 페이지 처리 과정

1. Client 의 요청을 **Controller**에서 **Model** 로 처리합니다.
    1. DB 조회가 필요하다면 DB 작업 후 처리한 데이터를 **Model**에 저장합니다.
2. Template engine(Thymeleaf) 에게 **View**, **Model** 전달합니다.
    1. **View**: 동적 HTML 파일
    2. **Model**: View 에 적용할 정보들
3. Template engine
    1. **View**에 **Model**을 적용 → 동적 웹페이지 생성
        1. 예) 로그인 성공 시, "로그인된 사용자의 Nickname"을 페이지에 추가
        2. Template engine 종류: 타임리프(Thymeleaf), Groovy, FreeMarker, Jade, JSP 등
4. Client(브라우저)에게 **View**(동적 웹 페이지, HTML)를 전달 해줍니다.

## 정적 페이지 처리 과정

일반적으로 SpringBoot 서버( `http://localhost:8080/파일명.html` )에 바로 요청하면 static폴더에서 찾아서 반환해줍니다.

만약 Controller를 통해 반환하는 것을 테스트하고 싶다면 implementation 'org.springframework.boot:spring-boot-starter-thymeleaf’ 해당 dependency를 주석 처리한 후 thymeleaf 는 동적 페이지 처리를 위한 템플릿 엔진이므로 추가하면 Controller에서 html파일 찾는 경로를 자동으로 설정합니다.

### **static** 폴더 @GetMapping

파일명을 문자열로 반환처리 하기

```java
@GetMapping("/static-hello")
public String hello() {
    return "hello.html";
}
```

주석 처리한 후 "hello.html" 이렇게 문자열로 반환하면 static 폴더의 해당 html 파일을 찾아 반환 해줍니다.

### **Redirect**

SpringBoot서버주소/html/redirect

```java
@GetMapping("/html/redirect")
public String htmlStatic() {
    return "redirect:/hello.html";
}
```

템플릿 엔진을 적용한 상태에서 static 폴더의 html 파일을 Controller를 통해서 처리하고 싶다면 이렇게 "redirect:/hello.html" redirect 요청을 문자열로 반환하면 SpringBoot서버주소/hello.html 요청이 재 수행되면서 static 폴더의 파일을 반환할 수 있습니다.

### Template engine 에 **View** 전달

SpringBoot서버주소/html/templates

```java
@GetMapping("/html/templates")
public String htmlTemplates() {
    return "hello";
}
```

타임리프 default 설정

- prefix: **classpath:/templates/**
- suffix: **.html**

/resources**/templates/**hello**.html**

static 폴더에 있는 html 파일을 바로 호출하는 방법이 가장 간단하지만 외부 즉, 브라우저에서 바로 접근하지 못하게 하고 싶거나 특정 상황에 Controller를 통해서 제어하고 싶다면 이렇게 templates 폴더에 해당 정적 html 파일을 추가하고 해당 html 파일명인  "hello" 문자열을 반환하여 처리할 수 있습니다. (.html은 생략가능!)
