# CascadeType 옵션

cascade 옵션은 ORM(객체-관계 매핑)에서 부모 엔티티가 자식 엔티티의 영속성을 관리하는 데 사용되는 기능입니다. 부모 엔티티의 cascade 옵션을 설정하면 부모 엔티티의 상태 변화가 자식 엔티티에도 영향을 미치게 됩니다. 즉, 부모 엔티티의 상태 변화에 따라 자식 엔티티의 영속성 상태를 자동으로 동기화하는 기능입니다.

부모-자식 엔티티가 있다고 가정했을때

```java
@Entity
public class Parent {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    @OneToMany(mappedBy = "parent", cascade = CascadeType.ALL)
    private List<Child> children;
}

@Entity
public class Child {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    @ManyToOne
    private Parent parent;
}
```

위의 코드에서 Parent 엔티티는 Child 엔티티와 일대다(OneToMany) 관계를 가지고 있습니다. Parent 엔티티의 children 필드에는 자식 엔티티들의 컬렉션이 저장되어 있습니다.

@OneToMany 어노테이션에 cascade = CascadeType.ALL 옵션을 설정했습니다. 이렇게 하면 Parent 엔티티의 상태가 변경될 때 해당 Parent와 연관된 모든 Child 엔티티들의 상태 변화도 자동으로 반영됩니다.

CascadeType 옵션에는 여러 가지 값을 사용할 수 있습니다. 일반적으로 사용되는 값들은 다음과 같습니다:

CascadeType.ALL: 모든 상태 변화에 대해 자식 엔티티에 적용됩니다. (INSERT, UPDATE, DELETE 등)
CascadeType.PERSIST: 부모 엔티티가 저장(PERSIST)될 때 자식 엔티티도 저장됩니다.
CascadeType.MERGE: 부모 엔티티가 병합(MERGE)될 때 자식 엔티티도 병합됩니다.
CascadeType.REMOVE: 부모 엔티티가 삭제(REMOVE)될 때 자식 엔티티도 삭제됩니다.
CascadeType.REFRESH: 부모 엔티티가 새로고침(REFRESH)될 때 자식 엔티티도 새로고침됩니다.
CascadeType.DETACH: 부모 엔티티가 분리(DETACH)될 때 자식 엔티티도 분리됩니다.
CascadeType 옵션을 사용하면 코드를 통해 각각의 자식 엔티티를 개별적으로 저장하거나 삭제하는 번거로움을 피할 수 있습니다. 부모 엔티티의 상태를 관리하는 동시에 자식 엔티티들도 함께 처리할 수 있으므로, 영속성 컨텍스트에서의 편리성과 코드의 간결성을 높일 수 있습니다.
