# 객체지향 프로그래밍_상속

## 01. 클래스간의 관계와 상속

상속의 사전적 정의는 부모가 자식에게 물려주는 행위 (== `확장`)

- 객체 지향 프로그램에서도 부모 클래스의 필드와 메서드를 자식 클래스에게 물려줄 수 있다.

- 상속을 사용하면 적은 양의 코드로 새로운 클래스를 작성할 수도 있고 공통적인 코드를 관리하여 코드의 추가와 변경이 쉬워질 수도 있다.

- 이러한 특성 때문에 상속을 사용하면 코드의 중복이 제거되고 재사용성이 크게 증가하여 생산성과 유지보수성에 매우 유리해진다.

🔑 클래스간의 상속은 `extends` 키워드를 사용하여 정의할 수 있다.

```java
public class 자식클래스 extends 부모클래스 {

}
```

1. 부모 클래스에 새로운 필드와 메서드가 추가되면 자식 클래스는 이를 상속받아 사용할 수 있다.

2. 자식 클래스에 새로운 필드와 메서드가 추가되어도 부모 클래스는 어떠한 영향도 받지 않는다.

3. 따라서 자식 클래스의 멤버 개수는 부모 클래스보다 항상 같거나 많다.

```java
public class Car {

    String company; // 자동차 회사
    private String model; // 자동차 모델
    private String color; // 자동차 색상
    private double price; // 자동차 가격

    double speed;  // 자동차 속도 , km/h
    char gear = 'P'; // 기어의 상태, P,R,N,D
    boolean lights; // 자동차 조명의 상태

    public String getModel() {
        return model;
    }

    public void setModel(String model) {
        this.model = model;
    }

    public double gasPedal(double kmh, char type) {
        changeGear(type);
        speed = kmh;
        return speed;
    }

    public double brakePedal() {
        speed = 0;
        return speed;
    }

    public char changeGear(char type) {
        gear = type;
        return gear;
    }

    public boolean onOffLights() {
        lights = !lights;
        return lights;
    }

    public void horn() {
        System.out.println("빵빵");
    }

}
```

```java
public class SportsCar extends Car{
    String engine;
    public void booster() {
        System.out.println("엔진 " + engine + " 부앙~\n");
    }
}
```

---

```java
public class Main {
    public static void main(String[] args) {
        // 부모 클래스 객체에서 자식 클래스 멤버 사용
        Car car = new Car();
        // car.engine = "Orion"; // 오류
        // car.booster(); // 오류

        // 자식 클래스 객체 생성
        SportsCar sportsCar = new SportsCar();
        sportsCar.engine = "Orion";
        sportsCar.booster();

        // 자식 클래스 객체에서 부모 클래스 멤버 사용
        sportsCar.company = "GENESIS";
        sportsCar.setModel("GV80");
        System.out.println("sportsCar.company = " + sportsCar.company);
        System.out.println("sportsCar.getModel() = " + sportsCar.getModel());
        System.out.println();

        sportsCar.horn();
        System.out.println(sportsCar.changeGear('D'));
    }
}
```

### `1) 클래스간의 관계`

클래스간의 관계를 분석하여 관계설정을 해줄 수 있습니다.

- 상속관계 : is - a (”~은 ~(이)다”)

- 포함관계 : has - a (”~은 ~을(를) 가지고 있다”)

#### **포함관계 예시**

- 자동차는 타이어를 가지고 있다.

- 자동차는 차문을 가지고 있다.

- 자동차는 핸들을 가지고 있다.

```java
public class Tire {
    String company; // 타이어 회사
    double price; // 타이어 가격

    public Tire(String company, double price) {
        this.company = company;
        this.price = price;
    }
}
```

```java
public class Door {
    String company; // 차문 회사
    String location; // 차문 위치, FL, FR, BL, BR

    public Door(String company, String location) {
        this.company = company;
        this.location = location;
    }
}
```

```java
public class Handle {
    String company; // 핸들 회사
    String type; // 핸들 타입

    public Handle(String company, String type) {
        this.company = company;
        this.type = type;
    }

    public void turnHandle(String direction) {
        System.out.println(direction + " 방향으로 핸들을 돌립니다.");
    }
}
```

```java
public class Car {

    static final String company = "GENESIS"; // 자동차 회사
    String model; // 자동차 모델
    String color; // 자동차 색상
    double price; // 자동차 가격

    double speed;  // 자동차 속도 , km/h
    char gear = 'P'; // 기어의 상태, P,R,N,D
    boolean lights; // 자동차 조명의 상태

    Tire[] tire;
    Door[] door;
    Handle handle;

    public Car(String model, String color, double price) {
        this.model = model;
        this.color = color;
        this.price = price;
    }

    public void setTire(Tire ... tire) {
        this.tire = tire;
    }

    public void setDoor(Door ... door) {
        this.door = door;
    }

    public void setHandle(Handle handle) {
        this.handle = handle;
    }

    public double gasPedal(double kmh, char type) {
        changeGear(type);
        speed = kmh;
        return speed;
    }

    public double brakePedal() {
        speed = 0;
        return speed;
    }

    public char changeGear(char type) {
        gear = type;
        return gear;
    }

    public boolean onOffLights() {
        lights = !lights;
        return lights;
    }

    public void horn() {
        System.out.println("빵빵");
    }
}
```

---

```java
public class Main {
    public static void main(String[] args) {
        // 자동차 객체 생성
        Car car = new Car("GV80", "Black", 50000000);

        // 자동차 부품 : 타이어, 차문, 핸들 선언
        Tire[] tires = new Tire[]{
                new Tire("KIA", 150000), new Tire("금호", 150000),
                new Tire("Samsung", 150000), new Tire("LG", 150000)
        };
        Door[] doors = new Door[]{
                new Door("LG", "FL"), new Door("KIA", "FR"),
                new Door("Samsung", "BL"), new Door("LG", "BR")
        };
        Handle handle = new Handle("Samsung", "S");

        // 자동차 객체에 부품 등록
        car.setTire(tires);
        car.setDoor(doors);
        car.setHandle(handle);

        // 등록된 부품 확인하기
        for (Tire tire : car.tire) {
            System.out.println("tire.company = " + tire.company);
        }
        System.out.println();

        for (Door door : car.door) {
            System.out.println("door.company = " + door.company);
            System.out.println("door.location = " + door.location);
            System.out.println();
        }
        System.out.println();

        // 자동차 핸들 인스턴스 참조형 변수에 저장
        Handle carHandle = car.handle;
        System.out.println("carHandle.company = " + carHandle.company);
        System.out.println("carHandle.type = " + carHandle.type + "\n");

        // 자동차 핸들 조작해보기
        carHandle.turnHandle("Right");
        carHandle.turnHandle("Left");
    }
}
```

### `2)단일 상속과 다중 상속`

Java는 다중상속을 허용하지 않는다

- 다중상속을 허용하면 클래스간의 관계가 복잡해지는 문제가 생기기 때문
- 만약 자식 클래스에서 상속받는 서로 다른 부모 클래스들이 같은 이름의 멤버를 가지고 있다면
자식 클래스에서는 이 멤버를 구별할 수 있는 방법이 없다는 문제 발생

```java
public final class Car {}
...
public class SportsCar extends Car{} // 오류가 발생합니다.
```

- 클래스에 final 키워드를 지정하여 선언하면 최종적인 클래스가 됨으로 더 이상 상속할 수 없음

```java
public class Car {
    public final void horn() {
        System.out.println("빵빵");
    }
}

...

public class SportsCar extends Car{
    public void horn() { // 오류가 발생합니다.
        super.horn();
    }
}
```

### `3) final`

- 메서드에 final 키워드를 지정하여 선언하면 최종적인 메서드가 됨으로 더 이상 오버라이딩할 수 없음

### `4) Object`

Object 는 말그대로 “객체”를 의미하는 단어이며 보통, Object 클래스를 의미

- Object 클래스는 Java 내 모든 클래스들의 최상위 부모 클래스

- 따라서, 모든 클래스는 Object의 메서드를 사용할 수 있다.

- 또한 부모 클래스가 없는 자식 클래스는 컴파일러에 의해 자동으로 Object 클래스를 상속받게 됨

- **Object 클래스의 메서드**

  - Object **clone()** : 해당 객체의 복제본을 생성하여 반환함.

  - boolean **equals(Object object)** : 해당 객체와 전달받은 객체가 같은지 여부를 반환함.

  - Class **getClass()** : 해당 객체의 클래스 타입을 반환함.

  - int **hashCode()** : 자바에서 객체를 식별하는 정수값인 해시 코드를 반환함.

  - String **toString()** : 해당 객체의 정보를 문자열
로 반환함. & Object 클래스에서는 클래스이름 @해쉬코드값 리턴함.

## 02. 오버라이딩

- 부모 클래스로부터 상속받은 메서드의 내용을 재정의 하는 것

- 부모 클래스의 메서드를 그대로 사용 가능하지만 자식 클래스의 상황에 맞게 변경을 해야하는 경우 오버라이딩을 사용

오버라이딩의 조건

  1. 선언부가 부모 클래스의 메서드와 일치해야 함

  2. 접근 제어자를 부모 클래스의 메서드 보다 좁은 범위로 변경할 수 없음

  3. 예외는 부모 클래스의 메서드 보다 많이 선언할 수 없음

```java
public class Car {

    String company; // 자동차 회사
    private String model; // 자동차 모델
    private String color; // 자동차 색상
    private double price; // 자동차 가격

    double speed;  // 자동차 속도 , km/h
    char gear = 'P'; // 기어의 상태, P,R,N,D
    boolean lights; // 자동차 조명의 상태

    public String getModel() {
    return model;
    }

    public void setModel(String model) {
    this.model = model;
    }

    public double gasPedal(double kmh, char type) {
    changeGear(type);
    speed = kmh;
    return speed;
    }

    public double brakePedal() {
    speed = 0;
    return speed;
    }

    public char changeGear(char type) {
    gear = type;
    return gear;
    }

    public boolean onOffLights() {
    lights = !lights;
    return lights;
    }

    public void horn() {
    System.out.println("빵빵");
    }

}
```

```java
public class SportsCar extends Car{
    String engine;
    public void booster() {
    System.out.println("엔진 " + engine + " 부앙~\n");
    }

    public SportsCar(String engine) {
    this.engine = engine;
    }

    @Override
    public double brakePedal() {
    speed = 100;
    System.out.println("스포츠카에 브레이크란 없다");
    return speed;
    }

    @Override
    public void horn() {
    booster();
    }
}
```

---

```java
public class Main {
    public static void main(String[] args) {
    // 부모 클래스 자동차 객체 생성
    Car car = new Car();
    car.horn(); // 경적

    System.out.println();
    // 자식 클래스 스포츠카 객체 생성
    SportsCar sportsCar = new SportsCar("Orion");

    // 오버라이딩한 brakePedal(), horn() 메서드 호출
    sportsCar.brakePedal();
    sportsCar.horn();

    }
}
```

### `1) super 와 super()`

#### **super**

super는 부모 클래스의 멤버를 참조할 수 있는 키워드

- 객체 내부 생성자 및 메서드에서 부모 클래스의 멤버에 접근하기 위해 사용될 수 있다
- 자식 클래스 내부에서 선언한 멤버와 부모 클래스에서 상속받은 멤버와 이름이 같을 경우 이를 구분하기 위해 사용된다.

```java
// 부모 클래스 Car
String model; // 자동차 모델
String color; // 자동차 색상
double price; // 자동차 가격
```

```java
// 자식 클래스 SportsCar
String model = "Ferrari"; // 자동차 모델
String color = "Red"; // 자동차 색상
double price = 300000000; // 자동차 가격
```

```java
public void setCarInfo(String model, String color, double price) {
super.model = model; // model은 부모 필드에 set
super.color = color; // color는 부모 필드에 set
this.price = price; // price는 자식 필드에 set
}
```

- 자식 클래스의 메서드를 호출하면 super 키워드로 접근한 부모 클래스의 model, color 필드에 매개변수의 값이 저장됩니다.
- this 키워드로 접근한 자식 클래스의 price 필드에는 매개변수의 값이 저장됩니다.

```java
public class Car {

    String company; // 자동차 회사
    String model; // 자동차 모델
    String color; // 자동차 색상
    double price; // 자동차 가격

    double speed;  // 자동차 속도 , km/h
    char gear = 'P'; // 기어의 상태, P,R,N,D
    boolean lights; // 자동차 조명의 상태

    public String getModel() {
        return model;
    }

    public String getColor() {
        return color;
    }

    public double gasPedal(double kmh, char type) {
        changeGear(type);
        speed = kmh;
        return speed;
    }

    public double brakePedal() {
        speed = 0;
        return speed;
    }

    public char changeGear(char type) {
        gear = type;
        return gear;
    }

    public boolean onOffLights() {
        lights = !lights;
        return lights;
    }

    public void horn() {
        System.out.println("빵빵");
    }

}
```

```java
public class SportsCar extends Car{
    String engine;

    String model = "Ferrari"; // 자동차 모델
    String color = "Red"; // 자동차 색상
    double price = 300000000; // 자동차 가격

    public SportsCar(String engine) {
        this.engine = engine;
    }

    public void booster() {
        System.out.println("엔진 " + engine + " 부앙~\n");
    }

    public void setCarInfo(String model, String color, double price) {
        super.model = model; // model은 부모 필드에 set
        super.color = color; // color는 부모 필드에 set
        this.price = price; // price는 자식 필드에 set
    }

    @Override
    public double brakePedal() {
        speed = 100;
        System.out.println("스포츠카에 브레이크란 없다");
        return speed;
    }

    @Override
    public void horn() {
        booster();
    }
}
```

---

```java
public class Main {
    public static void main(String[] args) {
        // 자식 클래스 스포츠카 객체 생성
        SportsCar sportsCar = new SportsCar("Orion");

        // 자식 객체의 model, color, price 초기값 확인
        System.out.println("sportsCar.model = " + sportsCar.model); // Ferrari
        System.out.println("sportsCar.color = " + sportsCar.color); // Red
        System.out.println("sportsCar.price = " + sportsCar.price); // 3.0E8
        System.out.println();

        // setCarInfo 메서드 호출해서 부모 및 자식 필드 값 저장
        sportsCar.setCarInfo("GV80", "Black", 50000000);

        // this.price = price; 결과 확인
        System.out.println("sportsCar.price = " + sportsCar.price); // 5.0E7
        System.out.println();

        // super.model = model; super.color = color;
        // 결과 확인을 위해 자식 클래스 필드 model, color 확인 & 부모 클래스 메서드인 getModel(), getColor() 호출
        // 자식 클래스 필드 값은 변화 없음.
        System.out.println("sportsCar.model = " + sportsCar.model); // Ferrari
        System.out.println("sportsCar.color = " + sportsCar.color); // Red
        System.out.println();

        // 부모 클래스 필드 값 저장됨.
        System.out.println("sportsCar.getModel() = " + sportsCar.getModel()); // GV80
        System.out.println("sportsCar.getColor() = " + sportsCar.getColor()); // Black

    }
}
```

#### **super()**

super(…)는 부모 클래스의 생성자를 호출할 수 있는 키워드

- 객체 내부 생성자 및 메서드에서 해당 객체의 부모 클래스의 생성자를 호출하기 위해 사용될 수 있다.

- 자식 클래스의 객체가 생성될 때 부모 클래스들이 모두 합쳐져서 하나의 인스턴스가 생성

- 이 때 부모 클래스의 멤버들의 초기화 작업이 먼저 수행

- 따라서 자식 클래스의 생성자에서는 부모 클래스의 생성자가 호출

- 또한 부모 클래스의 생성자는 가장 첫 줄에서 호출

```java
// 부모 클래스 Car 생성자
public Car(String model, String color, double price) {
this.model = model;
this.color = color;
this.price = price;
}
```

```java
// 자식 클래스 SportsCar 생성자
public SportsCar(String model, String color, double price, String engine) {
// this.engine = engine; // 오류 발생
super(model, color, price);
this.engine = engine;
}
```

- 자식 클래스 객체를 생성할 때 생성자 매개변수에 매개값을 받아와 super(…)를 사용해 부모 생성자의 매개변수에 매개값을 전달하여 호출하면서 부모 클래스의 멤버를 먼저 초기화

- 오버로딩된 부모 클래스의 생성자가 없다고 하더라도 부모 클래스의 기본 생성자를 호출

- 따라서 눈에 보이지는 않지만 컴파일러가 `super();` 를 자식 클래스 생성자 첫 줄에 자동으로 추가

```java
public class Car {

    String company; // 자동차 회사
    String model; // 자동차 모델
    String color; // 자동차 색상
    double price; // 자동차 가격

    double speed;  // 자동차 속도 , km/h
    char gear = 'P'; // 기어의 상태, P,R,N,D
    boolean lights; // 자동차 조명의 상태

    public Car(String model, String color, double price) {
        this.model = model;
        this.color = color;
        this.price = price;
    }

    public String getModel() {
        return model;
    }

    public String getColor() {
        return color;
    }

    public double getPrice() {
        return price;
    }

    public double gasPedal(double kmh, char type) {
        changeGear(type);
        speed = kmh;
        return speed;
    }

    public double brakePedal() {
        speed = 0;
        return speed;
    }

    public char changeGear(char type) {
        gear = type;
        return gear;
    }

    public boolean onOffLights() {
        lights = !lights;
        return lights;
    }

    public void horn() {
        System.out.println("빵빵");
    }

}
```

```java
public class SportsCar extends Car{
    String engine;

    public SportsCar(String model, String color, double price, String engine) {
            // this.engine = engine; // 오류 발생
        super(model, color, price);
        this.engine = engine;
    }

    public void booster() {
        System.out.println("엔진 " + engine + " 부앙~\n");
    }

    @Override
    public double brakePedal() {
        speed = 100;
        System.out.println("스포츠카에 브레이크란 없다");
        return speed;
    }

    @Override
    public void horn() {
        booster();
    }
}
```

---

```java
public class Main {
    public static void main(String[] args) {
        // 자식 클래스 스포츠카 객체를 생성합니다.
        SportsCar sportsCar = new SportsCar("Lamborghini", "Red", 400000000, "V12");
        sportsCar.brakePedal();
        sportsCar.horn();

        // 자식 클래스의 생성자를 통해 부모 클래스의 생성자가 호출되어 필드값이 초기화 되었는지 확인
        System.out.println("sportsCar.getModel() = " + sportsCar.getModel()); // Lamborghini
        System.out.println("sportsCar.getColor() = " + sportsCar.getColor()); // Red
        System.out.println("sportsCar.getPrice() = " + sportsCar.getPrice()); // 4.0E8

    }
}
```

## 03. 다형성

### `1) 참조변수의 타입변환`

`부모타입 변수 = 자식타입객체;` 는 자동으로 부모타입으로 변환이 일어난다.

- 자식 객체는 부모 객체의 멤버를 상속받기 때문에 부모와 동일하게 취급될 수 있다.

- 예를 들어 포유류 클래스를 상속받은 고래 클래스가 있다면 `포유류 고래 = 고래객체;` 가 성립될 수 있다.

- 왜냐하면 고래 객체는 포유류의 특징인 모유수유 행위를 가지고 있기 때문이다.

- 다만 주의할 점은 부모타입 변수로 자식객체의 멤버에 접근할 때는 부모 클래스에 선언된 즉, 상속받은 멤버만 접근할 수 있다.

```java
class Mammal {
    // 포유류는 새끼를 낳고 모유수유를 한다.
    public void feeding() {
        System.out.println("모유수유를 합니다.");
    }
}
```

```java
class Whale extends Mammal {
    // 고래는 포유류 이면서 바다에 살며 수영이 가능하다.
    public void swimming() {
        System.out.println("수영하다.");
    }

    @Override
    public void feeding() {
        System.out.println("고래는 모유수유를 합니다.");
    }
}
```

---

```java
public class Main {
    public static void main(String[] args) {
        // 고래는 포유류이기 때문에 포유류 타입으로 변환될 수 있습니다.
        Mammal mammal = new Whale();

        // 하지만 포유류 전부가 바다에 살고 수영을 할 수 있는 것은 아니기 때문에
        // 수영 하다 메서드는 실행 불가
        // 즉, 부모 클래스에 swimming이 선언되어있지 않아서 사용 불가능합니다.
        // mammalia.swimming(); // 오류 발생

        // 반대로 모든 포유류가 전부 고래 처럼 수영이 가능한 것이 아니기 때문에 타입변환이 불가능합니다.
        // 즉, 부모타입의 객체는 자식타입의 변수로 변환될 수 없습니다.
        // Whale whale = new Mammal(); // 오류 발생

        mammal.feeding();
    }
}
```

### `2) 강제 타입변환`

`자식타입 변수 = (자식타입) 부모타입객체;`

- 부모타입객체는 자식타입 변수로 자동으로 타입변환되지 않습니다.

- 이럴때는 (자식타입) 즉, 타입변환 연산자를 사용하여 강제로 자식타입으로 변환할 수 있습니다.

```java
// 자식타입객체가 자동 타입변환된 부모타입의 변수
Mammal mammal = new Whale();
mammal.feeding();

// 자식객체 고래의 수영 기능을 사용하고 싶다면
// 다시 자식타입으로 강제 타입변환을 하면된다.
Whale whale = (Whale) mammal;
whale.swimming();
```

- 다만 무조건 강제 타입변환을 할 수 있는 것은 아닙니다.

- 자식타입객체가 부모타입으로 자동 타입변환된 후 다시 자식타입으로 변환될 때 만 강제 타입변환이 가능합니다.

- 부모타입 변수로는 자식타입객체의 고유한 멤버를 사용할 수 없기 때문에 사용이 필요한 경우가 생겼을 때 강제 타입변환을 사용합니다.

```java
Mammal newMammal = new Mammal();
Whale newWhale = (Whale) newMammal; // ClassCastException 발생
```

- 이렇게 자동 타입변환된 부모타입 변수가 아닌 부모객체를 자식타입의 변수로 강제 타입변환하려고 하면 오류가 발생한다.

```java
class Mammal {
    // 포유류는 새끼를 낳고 모유수유를 한다.
    public void feeding() {
        System.out.println("모유수유를 합니다.");
    }
}
```

```java
class Whale extends Mammal {
    // 고래는 포유류 이면서 바다에 살며 수영이 가능하다.
    public void swimming() {
        System.out.println("수영하다.");
    }

    @Override
    public void feeding() {
        System.out.println("고래는 모유수유를 합니다.");
    }
}
```

---

```java
public class Main {
    public static void main(String[] args) {
        // 자동 타입변환된 부모타입의 변수의 자식 객체
        Mammal mammal = new Whale();
        mammal.feeding();

        // 자식객체 고래의 수영 기능을 사용하고 싶다면
        // 다시 자식타입으로 강제 타입변환을 하면된다.
        Whale whale = (Whale) mammal;
        whale.swimming();

        Mammal newMammal = new Mammal();
        // Whale newWhale = (Whale) newMammal;
    }
}
```

### `3) 다형성이란?`

 다형성이란 ‘여러 가지 형태를 가질 수 있는 능력’을 의미합니다.

- 예를 들어 자동차의 핸들을 교체하면 핸들링이 부드러워지고 바퀴를 교체하면 승차감이 좋아집니다.

- 소프트웨어 또한 구성하고 있는 객체를 바꿨을 때 소프트웨어의 실행 성능 및 결과물이 다르게 나올 수 있습니다.

- 일전에 배운 참조변수 타입변환을 활용해서 다형성을 구현할 수 있습니다.

```java
Tire tire = new HankookTire("HANKOOK");
Tire tire = new KiaTire("KIA");
```

- `부모타이어 변수 = 자식타이어객체;` 를 선언하여 자동 타입변환된 변수를 사용하여 각각의 자식타이어 객체에 재정의 된 메서드를 통해 다양한 승차감을 가진 자동차를 생성할 수 있습니다.

```java
public Car(Tire tire) {
this.tire = tire;
}

...

Car car1 = new Car(new KiaTire("KIA"));
Car car2 = new Car(new HankookTire("HANKOOK"));
```

- 매개변수에도 다형성이 적용될 수 있습니다.

- Car 생성자에서 매개변수의 타입이 부모 타이어 이기 때문에 자식 타이어 객체들을 매개값으로 전달할 수 있습니다.

```java
Tire getHankookTire() {
return new HankookTire("HANKOOK");
}

Tire getKiaTire() {
return new KiaTire("KIA");
}

...

Tire hankookTire = car1.getHankookTire();
KiaTire kiaTire = (KiaTire) car2.getKiaTire();
```

- 반환타입에도 다형성이 적용될 수 있습니다.

- 반환타입이 부모 타이어 이기 때문에 자식 타이어 객체들을 반환값으로 지정할 수 있습니다.

- 또한 자동 타입변환이된 반환값인 자식 타이어 객체를 강제 타입변환할 수도 있습니다.

```java
public class Tire {
    String company; // 타이어 회사

    public Tire(String company) {
        this.company = company;
    }

    public void rideComfort() {
        System.out.println(company + " 타이어 승차감은?");
    }
}
```

```java
public class KiaTire extends Tire{

    public KiaTire(String company) {
        super(company);
    }

    @Override
    public void rideComfort() {
        System.out.println(super.company + " 타이어 승차감은 " + 60);
    }
}
```

```java
public class HankookTire extends Tire {

    public HankookTire(String company) {
        super(company);
    }

    @Override
    public void rideComfort() {
        System.out.println(super.company + " 타이어 승차감은 " + 100);
    }
}
```

```java
public class Car {
    Tire tire;

    public Car(Tire tire) {
        this.tire = tire;
    }

    Tire getHankookTire() {
        return new HankookTire("HANKOOK");
    }

    Tire getKiaTire() {
        return new KiaTire("KIA");
    }
}
```

---

```java
public class Main {
    public static void main(String[] args) {
        // 매개변수 다형성 확인!
        Car car1 = new Car(new KiaTire("KIA"));
        Car car2 = new Car(new HankookTire("HANKOOK"));

        // 반환타입 다형성 확인!
        Tire hankookTire = car1.getHankookTire();
        KiaTire kiaTire = (KiaTire) car2.getKiaTire();

        // 오버라이딩된 메서드 호출
        car1.tire.rideComfort(); // KIA 타이어 승차감은 60
        car2.tire.rideComfort(); // HANKOOK 타이어 승차감은 100
    }
}
```

### `4) instanceof`

다형성 기능으로 인해 해당 클래스 객체의 원래 클래스명을 체크하는것이 필요한데 이때 사용할 수 있는 명령어가 `instance of` 입니다.

- 이 명령어를 통해서 해당 객체가 내가 의도하는 클래스의 객체인지 확인할 수 있습니다.
- `{대상 객체}` `instance of` `{클래스 이름}` 와 같은 형태로 사용하면 응답값은 boolean 입니다.

```java
// 다형성

class Parent { }
class Child extends Parent { }
class Brother extends Parent { }

public class Main {
    public static void main(String[] args) {

            Parent pc = new Child();  // 다형성 허용 (자식 -> 부모)

    Parent p = new Parent();

    System.out.println(p instanceof Object); // true 출력
    System.out.println(p instanceof Parent); // true 출력
    System.out.println(p instanceof Child);  // false 출력

    Parent c = new Child();

    System.out.println(c instanceof Object); // true 출력
    System.out.println(c instanceof Parent); // true 출력
    System.out.println(c instanceof Child);  // true 출력

    }
}
```

## 04. 추상 클래스

### `1) 추상 클래스란?`

클래스가 설계도라면 추상 클래스는 미완성된 설계도입니다.

- abstract 키워드를 사용하여 추상 클래스를 선언할 수 있습니다.

```java
public abstract class 추상클래스명 {

}
```

- 추상 클래스는 추상 메서드를 포함할 수 있습니다.
- 추상 메서드가 없어도 추상 클래스로 선언할 수 있습니다.
- 추상 클래스는 자식 클래스에 상속되어 자식 클래스에 의해서만 완성될 수 있습니다.
- 추상 클래스는 여러개의 자식 클래스들에서 공통적인 필드나 메서드를 추출해서 만들 수 있습니다.

### `2) 추상 메서드`

추상 메서드는 아직 구현되지 않은 미완성된 메서드입니다.

- abstract 키워드를 사용하여 추상 메서드를 선언할 수 있습니다.

```java
public abstract class 추상클래스명 {
    abstract 리턴타입 메서드이름(매개변수, ...);
}
```

- 추상 메서드는 일반적인 메서드와는 다르게 블록{ }이 없습니다.
- 즉, 정의만 할 뿐, 실행 내용은 가지고 있지 않습니다.

- 추상 클래스 상속

추상 메서드는 `extends` 키워드를 사용하여 클래스에서 상속됩니다.

```java
public class 클래스명 extends 추상클래스명 {
    @Override
    public 리턴타입 메서드이름(매개변수, ...) {
        // 실행문
    }
}
```

- 상속받은 클래스에서 추상 클래스의 추상 메서드는 반드시 오버라이딩 되어야 합니다.

- 추상 클래스 사용방법

클래스들의 공통적인 필드와 메서드를 추출합니다.

- BenzCar

```java
public class BenzCar {
String company; // 자동차 회사 : GENESIS
String color; // 자동차 색상
double speed;  // 자동차 속도 , km/h

    public double gasPedal(double kmh) {
    speed = kmh;
    return speed;
    }

    public double brakePedal() {
    speed = 0;
    return speed;
    }

    public void horn() {
    System.out.println("Benz 빵빵");
    }

}
```

- AudiCar

```java
public class AudiCar {
String company; // 자동차 회사 : GENESIS
String color; // 자동차 색상
double speed;  // 자동차 속도 , km/h

    public double gasPedal(double kmh) {
    speed = kmh;
    return speed;
    }

    public double brakePedal() {
    speed = 0;
    return speed;
    }

    public void horn() {
    System.out.println("Audi 빵빵");
    }

}
```

- ZenesisCar

```java
public class ZenesisCar {
String company; // 자동차 회사 : GENESIS
String color; // 자동차 색상
double speed;  // 자동차 속도 , km/h

    public double gasPedal(double kmh) {
    speed = kmh;
    return speed;
    }

    public double brakePedal() {
    speed = 0;
    return speed;
    }

    public void horn() {
    System.out.println("Zenesis 빵빵");
    }

}
```

- Car

```java
public abstract class Car {
String company; // 자동차 회사 : GENESIS
String color; // 자동차 색상
double speed;  // 자동차 속도 , km/h

    public double gasPedal(double kmh) {
    speed = kmh;
    return speed;
    }

    public double brakePedal() {
    speed = 0;
    return speed;
    }

    public abstract void horn();
}
```

- BenzCar, AudiCar, ZenesisCar 는 horn() 메서드의 내용에 차이가 존재합니다.
- 따라서 horn() 메서드를 추상 메서드로 선언하여 자식 클래스에서 재정의 될 수 있도록 합니다.

```java
public class BenzCar extends Car {

    @Override
    public void horn() {
        System.out.println("Benz 빵빵");
    }
}
```

```java
public class AudiCar extends Car {

    @Override
    public void horn() {
        System.out.println("Audi 빵빵");
    }
}
```

```java
public class ZenesisCar extends Car {

    @Override
    public void horn() {
        System.out.println("Zenesis 빵빵");
    }
}
```

```java
public abstract class Car {
    String company; // 자동차 회사
    String color; // 자동차 색상
    double speed;  // 자동차 속도 , km/h

    public double gasPedal(double kmh) {
        speed = kmh;
        return speed;
    }

    public double brakePedal() {
        speed = 0;
        return speed;
    }

    public abstract void horn();
}
```

---

```java
public class Main {
    public static void main(String[] args) {
        Car car1 = new BenzCar();
        car1.horn();
        System.out.println();

        Car car2 = new AudiCar();
        car2.horn();
        System.out.println();

        Car car3 = new ZenesisCar();
        car3.horn();
    }
}
```
