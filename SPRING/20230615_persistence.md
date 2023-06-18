# Persistence ?

Persistence를 한글로 번역하면 `영속성`, `지속성` 이라는 뜻이 됩니다.
  
  > Persistence를 객체의 관점으로 해석해 보자면 ‘**객체가 생명(객체가 유지되는 시간)이나 공간(객체의 위치)을 자유롭게 유지하고 이동할수 있는 객체의 성질**’을 의미합니다.
  >
영속성 컨텍스트를 좀 더 쉽게 표현해 보자면 **Entity 객체를 효율적으로 쉽게 관리하기 위해 만들어진 공간**입니다.

JPA를 사용하면 SQL을 작성하지 않아도 DB를 저장 및 조회 수정 삭제하고 이런 일련의 과정을 효율적으로 처리하기 위해 JPA는 영속성 컨텍스트에 Entity객체들을 저장하여 관리하면서 DB와 소통합니다.

## **EntityManager**

영속성 컨텍스트에 접근하여 Entity 객체들을 조작하기 위해서는 `EntityManager`가 필요합니다.

> EntityManager는 이름 그대로 Entity를 관리하는 관리자입니다.
>

개발자들은 EntityManager를 사용해서 Entity를 저장하고 조회하고 수정하고 삭제할 수 있습니다.
EntityManager는 `EntityManagerFactory`를 통해 생성하여 사용할 수 있습니다.

## **EntityManagerFactory**

`EntityManagerFactory`는 일반적으로 **DB 하나에 하나만 생성**되어 **애플리케이션이 동작하는 동안 사용**됩니다.

EntityManagerFactory를 만들기 위해서는 DB에 대한 정보를 전달해야합니다.

정보를 전달하기 위해서는 `/resources/META-INF/`  위치에 `persistence.xml` 파일을 만들어 정보를 넣어두면 됩니다.
