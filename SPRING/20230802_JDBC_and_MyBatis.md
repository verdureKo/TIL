# JDBC(JAVA Database Connectivity)와 MyBatis

모두 JDBC를 기반으로 한 데이터베이스 액세스를 간편하게 해주는 라이브러리 또는 프레임워크입니다.

## 1. 스프링 부트 라이브러리

### **JDBC (Java Database Connectivity)**

JDBC Template은 스프링 프레임워크의 일부로, 스프링의 JdbcTemplate 클래스를 통해 제공됩니다. JDBC Template은 순수 JDBC 코드를 작성하는 번거로움을 줄이고, 데이터베이스 액세스를 단순화하기 위해 만들어졌습니다.

특징:

- 템플릿 기반 접근: JDBC Template은 템플릿 기반의 디자인 패턴을 사용하여 데이터베이스 액세스를 처리합니다. 개발자는 간단한 템플릿 메서드를 사용하여 데이터베이스 작업을 수행할 수 있습니다.
- 자동 리소스 관리: JDBC Template은 데이터베이스 리소스의 연결 및 해제와 같은 작업을 자동으로 처리합니다.
- 반복적인 코드 감소: JDBC Template을 사용하면 데이터베이스 액세스에 대한 반복적인 코드를 줄일 수 있습니다.
- 스프링 통합: 스프링 프레임워크와 통합되어 스프링 애플리케이션에서 편리하게 사용할 수 있습니다.

단점:

- SQL과의 강력한 결합: SQL 쿼리를 직접 작성하여 데이터베이스와 상호작용하기 때문에, SQL과의 강력한 결합이 발생할 수 있습니다.

### **MyBatis**

MyBatis는 `데이터베이스 액세스 계층을 자동화`하기 위해 개발된 자바 ORM(Object-Relational Mapping) 프레임워크입니다. 기존 JDBC 코드의 반복적인 작성과 SQL과의 결합을 줄여 개발자가 데이터베이스와 상호작용할 수 있도록 합니다.

특징:

- 객체-관계 매핑 (ORM): MyBatis는 객체와 데이터베이스 테이블 간의 매핑을 자동으로 처리하여 순수한 자바 객체를 사용하여 데이터베이스를 조작할 수 있도록 합니다.
- 외부 XML 설정 파일: MyBatis는 SQL 쿼리와 데이터베이스 매핑을 위한 외부 XML 설정 파일을 사용합니다. 이를 통해 SQL과 자바 코드를 분리하여 관리할 수 있습니다.
- 유연한 SQL 작성: 개발자는 MyBatis의 동적 쿼리 기능을 활용하여 동적으로 SQL을 작성하고 실행할 수 있습니다.
- 높은 커스터마이징 가능성: MyBatis는 다양한 설정 옵션과 사용자 정의 매퍼를 통해 개발자가 높은 수준의 커스터마이징이 가능합니다

단점:

- 학습 곡선: MyBatis를 사용하기 위해서는 초기 학습 곡선이 있을 수 있습니다.
- 일부 성능 저하: 순수한 JDBC와 비교할 때 일부 성능 저하가 발생할 수 있으나, 대부분의 상황에서는 이를 감수할 만한 편의성과 유연성을 제공합니다.

결론적으로, JDBC Template은 `스프링 프레임워크와 간단한 데이터베이스 액세스`에 사용되며, MyBatis는 객체-관계 매핑과 유연한 SQL 작성을 지원하여 `더 복잡한 데이터베이스 액세스를 관리`하기 위해 사용됩니다. 프로젝트의 요구사항과 개발자의 선호도에 따라 적절한 도구를 선택하는 것이 중요합니다.

## MyBatis는 SQL 쿼리를 생성하는 두 가지 주요 방법

### **1. XML Mapper 파일을 사용한 정적 SQL**

MyBatis의 첫 번째 방법은 XML Mapper 파일을 사용하여 정적인 SQL 쿼리를 정의하는 것입니다. 이 방법은 주로 복잡한 SQL 쿼리를 관리하고 관계형 데이터베이스와의 상호작용을 처리하는데 유용합니다.

```xml
<!-- Select User by ID -->
<select id="getUserById" parameterType="int" resultType="User">
  SELECT id, username, email
  FROM users
  WHERE id = #{id}
</select>

<!-- Insert User -->
<insert id="insertUser" parameterType="User">
  INSERT INTO users (username, email)
  VALUES (#{username}, #{email})
</insert>
```

UserMapper.xml 예시

- **XML Mapper 파일의 장점:**
  - SQL과 자바 코드의 분리: XML Mapper 파일을 사용하면 SQL 쿼리를 자바 코드에서 완전히 분리할 수 있습니다. 이는 유지보수 측면에서 유용하며, 복잡한 쿼리를 보다 체계적으로 관리할 수 있습니다.
  - 동적 쿼리 지원: XML Mapper 파일을 사용하면 동적 쿼리를 작성하는 데 더 적합합니다. 조건에 따라 쿼리가 동적으로 변경되어야 하는 경우 유연하게 처리할 수 있습니다.
  - 재사용성: XML Mapper 파일에 정의된 쿼리들은 여러 인터페이스에서 재사용할 수 있습니다. 이는 코드 중복을 방지하고 생산성을 향상시킵니다.

- **XML Mapper 파일의 단점:**
  - 학습 곡선: XML 기반의 설정 파일을 다루는 데 익숙하지 않은 개발자들은 초기 학습 곡선이 있을 수 있습니다.
  - 디버깅 어려움: XML 파일에 쿼리가 정의되어 있기 때문에, 쿼리에 오류가 발생하면 디버깅이 어려울 수 있습니다.

### **2. 어노테이션을 사용한 동적 SQL**

MyBatis의 두 번째 방법은 Java 어노테이션을 사용하여 동적인 SQL 쿼리를 생성하는 것입니다. 이 방법은 간단한 쿼리나 프로시저와 같이 더 단순한 쿼리를 처리하는데 적합합니다.
Java 인터페이스에서 메서드를 정의하고, 어노테이션을 통해 SQL 쿼리를 작성합니다.

```java
public interface UserMapper {

  @Select("SELECT id, username, email FROM users WHERE id = #{id}")
  User getUserById(int id);

  @Insert("INSERT INTO users (username, email) VALUES (#{username}, #{email})")
  void insertUser(User user);
}
```

UserMapper.java 예시

- **어노테이션 방식의 장점:**
  - 간결하고 직관적: 어노테이션 방식은 쿼리를 Java 인터페이스의 메서드에 바로 작성하기 때문에 간결하고 직관적입니다. 특히 간단한 쿼리의 경우 빠르게 작성할 수 있습니다.
  - 빠른 시작: XML 파일을 생성하고 관리하는데 드는 번거로움이 없으므로, 프로젝트를 빠르게 시작할 수 있습니다.

- **어노테이션 방식의 단점:**
  - SQL과 자바 코드 결합: 어노테이션 방식은 SQL 쿼리를 자바 코드에 직접 작성하므로, SQL과 자바 코드의 결합이 강화됩니다. 이는 유지보수 측면에서 부적절한 SQL 수정으로 인한 영향을 받을 수 있습니다.
  - 동적 쿼리 제한: 어노테이션 방식은 동적 쿼리 작성을 XML Mapper 파일보다 제한적으로 처리합니다. 복잡한 동적 쿼리의 경우 XML 파일보다 유연성이 떨어질 수 있습니다.

MyBatis는 두 가지 방법을 혼용하여 사용할 수 있으며, 프로젝트의 복잡성과 쿼리의 유형에 따라 적절한 방식을 선택하면 됩니다.
