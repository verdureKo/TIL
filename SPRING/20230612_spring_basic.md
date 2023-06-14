# Spring 기초

👨‍🦲 곧.. 난 머머리가 될것이다.

## Spring ?

Spring은 2004년에 1.0이 등장한 이후 20년가까이 가장 사랑받고있는 코드 및 구성을 간소화할 수 있는  매우 강력한 모듈식 프레임워크입니다.

Spring 프레임워크는 `AOP`, `IoC/DI` 등과 같은 아주 강력한 핵심 기능들을 가지고 있습니다.

## Spring Boot ?

핵심 기능을 사용하기 위해서는 아주 많은 xml 설정들이 필요했지만 2014년 `SpringBoot` 가 등장했습니다.

SpringBoot는 기존의 무겁고 작성하기 힘들던 xml 대신에 Java의 `@애너테이션` 기반의 설정을 적극적으로 사용하고 있기 때문에 아주 간편하게 핵심 기능들을 사용할 수 있습니다.

일반적인 개발에 필요한 기본 설정들을 default로 값이 설정되어 자동으로 설계되도록 되어있습니다.

또한 외부 라이브러리나 하위 프레임워크들의 의존성 관리가 매우 쉬워졌습니다.

[Spring QuickStart Guide](https://spring.io/quickstart) 👈스프링 부트 가이드

이전처럼 각각의 버전 호환성을 직접 확인할 필요없이 `Spring-boot-starter-web`처럼 필요한 외부 라이브러리들과 프레임워크들은 의존성에 맞게 묶어 제공해줍니다.

마지막으로 SpringBoot의 강력한 점은 바로 `내장 Apache Tomcat` 입니다.
Spring 프레임워크에서는 서버를 실행시키기 위해 Apache Tomcat을 직접 다운로드 받고 설정하고 프로젝트에 삽입해야하는 번거로움이 있었지만 SpringBoot에서는 기본적으로 starter-web dependency를 설정하면 자동으로 내장형 Apache Tomcat을 제공해 줍니다.

## Spring MVC?

Servlet API를 기반으로 구축된 독창적인 웹 프레임워크로, 처음부터 Spring Framework에 포함되어 왔으며, 정식 명칭인 "Spring Web MVC"는 소스 모듈(spring-webmvc)의 이름에서 따왔으나,  "Spring MVC"로 더 일반적으로 알려져 있다.
[Spring 공식문서](https://docs.spring.io/spring-framework/reference/web/webmvc.html)

MVC란 Model-View-Controller의 약자로, 소프트웨어 디자인 패턴 중 하나이다.

MVC 패턴은 소프트웨어를 구성하는 요소들을 Model, View, Controller로 구분하여 각각의 역할을 분리한다.

MVC 패턴은 소프트웨어를 구성하는 요소들을 분리함으로써 코드의 재사용성과 유지보수성을 높이고, 개발자들 간의 협업을 용이하게 합니다. 따라서 소프트웨어를 개발할 때, MVC 패턴을 적용하여 구조를 잘 설계하는 것이 중요하다.

### **Model**

- 데이터와 비즈니스 로직을 담당한다.
- 데이터베이스와 연동하여 데이터를 저장하고 불러오는 등의 작업을 수행한다.

### **View**

- 사용자 인터페이스를 담당한다.
- 사용자가 보는 화면과 버튼, 폼 등을 디자인하고 구현한다.

### **Controller**

- Model과 View 사이의 상호작용을 조정하고 제어한다.
- 사용자의 입력을 받아 Model에 전달하고, Model의 결과를 바탕으로 View를 업데이트한다.
