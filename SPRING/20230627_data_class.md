# Spring Data Class

## DAO(Data Access Object)

데이터 사용기능 담당 클래스이다. DB 데이터 조회나 수정, 입력, 삭제와 같은 로직을 처리하기 위해 사용한다. CRUD의 기능을 한다고 보면 된다. DAOInterface/DAOImplement 로 구분지어 명세와 구현 분리하며 개발한다.
만약 Mybatis연동 때처럼 Interface만 필요한 경우 그냥 DAO라고 명시할 수 있다.

## DTO(Data Transfer Object)

데이터 저장 담당 클래스이다. Controller, Service, View처럼 계층 간의 데이터 교환을 위해 쓰인다. 로직을 갖고 있지 않으며 순수한 데이터 객체이며 getter, setter 메소드만을 갖고 있다.

## VO(Value Object)

DTO와 마찬가지로 데이터 저장 담당 클래스이다. DTO와는 다르게 VO는 값을 위해 쓰이는 객체로 Ready-Only 속성을 갖고 있다. 그렇기 때문에 getter 기능만을 포함하고 있다.

## BO(Business Object)

VO와 마찬가지로 데이터 저장 담당 클래스이다. 근데 비즈니스 로직을 포함하고 있다. 즉, 비즈니스 관련 내용을 담은 VO라고 생각하면 될듯 하다.
