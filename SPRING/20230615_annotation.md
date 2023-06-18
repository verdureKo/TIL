# SpringBoot의 Annotation

- **@Entity** : JPA가 관리할 수 있는 Entity 클래스로 지정할 수 있습니다.
  - **@Entity(name = "Memo") :** Entity 클래스 이름을 지정할 수 있습니다. (default: 클래스명)
  - JPA가 Entity 클래스를 인스턴스화 할 때 기본 생성자를 사용하기 때문에 반드시 현재 Entity 클래스에서 기본 생성자가 생성되고 있는지 확인해야 합니다.
- **@Table** : 매핑할 테이블을 지정해줍니다.
  - **@Table(name = "memo") :** 매핑할 테이블의 이름을 지정할 수 있습니다. (default: Entity 명)
- **@Column** :
  - **@Column(name = "username") :** 필드와 매핑할 ****테이블의 컬럼을 지정할 수 있습니다. (default: 객체의 필드명)
  - **@Column(nullable =  false) :** 데이터의 null 값 허용 여부를 지정할 수 있습니다. (default: true)
  - **@Column(unique = true) :** 데이터의 중복 값 허용 여부를 지정할 수 있습니다. (default: false)
  - **@Column(length =  500) :** 데이터 값(문자)의 길이에 제약조건을 걸 수 있습니다. (default: 255)
- **@Id** : 테이블의 기본 키를 지정해줍니다.
  - 이 기본 키는 영속성 컨텍스트에서 Entity를 구분하고 관리할 때 사용되는 식별자 역할을 수행합니다.
    - 따라서 기본 키 즉, 식별자 값을 넣어주지 않고 저장하면 오류가 발생합니다.
  - **@Id** 옵션만 설정하면 기본 키 값을 개발자가 직접 확인하고 넣어줘야 하는 불편함이 발생합니다.
  
- **@GeneratedValue** 옵션을 ****추가하면 기본 키 생성을 DB에 위임할 수 있습니다.

```java
@Entity // JPA가 관리할 수 있는 Entity 클래스 지정
@Table(name = "memo") // 매핑할 테이블의 이름을 지정
public class Memo {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    // nullable: null 허용 여부
    // unique: 중복 허용 여부 (false 일때 중복 허용)
    @Column(name = "username", nullable = false, unique = true)
    private String username;

    // length: 컬럼 길이 지정
    @Column(name = "contents", nullable = false, length = 500)
    private String contents;
}
```

- **@GeneratedValue(strategy = GenerationType**.**IDENTITY)**
  - `id bigint not null auto_increment` : **auto_increment** 조건이 추가된 것을 확인할 수 있습니다.
  - 해당 옵션을 추가해주면 개발자가 직접 id 값을 넣어주지 않아도 자동으로 순서에 맞게 기본 키가 추가됩니다.

## **JPA Auditing** 적용하기

- Timestamped

📌 데이터의 생성(created_at), 수정(modified_at) 시간은
포스팅, 게시글, 댓글 등 다양한 데이터에 매우 자주 활용됩니다.
각각의 Entity의 생성 수정 시간을 매번 작성하는건 너무 비효율적입니다.

```java
@Getter
@MappedSuperclass
@EntityListeners(AuditingEntityListener.class)
  public abstract class Timestamped {

    @CreatedDate
    @Column(updatable = false)
    @Temporal(TemporalType.TIMESTAMP)
      private LocalDateTime createdAt;

      @LastModifiedDate
      @Column
      @Temporal(TemporalType.TIMESTAMP)
      private LocalDateTime modifiedAt;
}
```

- **Spring Data JPA**에서는 시간에 대해서 자동으로 값을 넣어주는 기능인 `JPA Auditing`을 제공하고 있습니다.
- **@MappedSuperclass**
- JPA Entity 클래스들이 해당 추상 클래스를 상속할 경우 createdAt, modifiedAt 처럼 추상 클래스에 선언한 멤버변수를 컬럼으로 인식할 수 있습니다.
- **@EntityListeners(AuditingEntityListener.class)**
- 해당 클래스에 Auditing 기능을 포함시켜 줍니다.
- **@CreatedDate**
- Entity 객체가 생성되어 저장될 때 시간이 자동으로 저장됩니다.
- 최초 생성 시간이 저장되고 그 이후에는 수정되면 안되기 때문에 `updatable = false` 옵션을 추가합니다.
- **@LastModifiedDate**
- 조회한 Entity 객체의 값을 변경할 때 변경된 시간이 자동으로 저장됩니다.
- 처음 생성 시간이 저장된 이후 변경이 일어날 때마다 해당 변경시간으로 업데이트됩니다.
- **@Temporal**
- 날짜 타입(java.util.Date, java.util.Calendar)을 매핑할 때 사용합니다.
- DB에는 Date(날짜), Time(시간), Timestamp(날짜와 시간)라는 세 가지 타입이 별도로 존재합니다.
- **DATE : ex) 2023-01-01**
- **TIME : ex) 20:21:14**
- **TIMESTAMP : ex) 2023-01-01 20:22:38.771000**

⚠️ `@SpringBootApplication` 이 있는 class에 `@EnableJpaAuditing` 추가!

- JPA Auditing 기능을 사용하겠다는 정보를 전달해주기 위해 `@EnableJpaAuditing` 을 추가해야합니다.
