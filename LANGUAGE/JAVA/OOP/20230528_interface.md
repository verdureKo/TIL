# 객체지향 프로그래밍_인터페이스

## 01. 인터페이스의 역할

- 인터페이스는 두 객체를 연결해주는 다리 역할
- 사람 객체는 멀티 리모컨 인터페이스를 통해서 삼성티비 객체의 채널을 변경할 수 있다.
- 이때 삼성티비가 아니라 엘지티비로 객체가 교체된다고 해도 채널을 변경할 수 있다.
- 상속 관계가 없는 다른 클래스들이 서로 동일한 행위 즉, 메서드를 구현해야할 때 인터페이스는 구현 클래스들의 동일한 사용 방법과 행위를 보장해 줄 수 있다.
- 인터페이스는 스팩이 정의된 메서드들의 집합이다.
- 인터페이스의 구현 클래스들은 반드시 정의된 메서드들을 구현해야한다.
- 따라서 구현 클래스들의 동일한 사용 방법과 행위를 보장해 줄 수 있다.
- 이러한 특징은 인터페이스에 다형성을 적용할 수 있게 만들어 준다.

### `1) 인터페이스 선언`

interface 키워드를 사용하여 인터페이스를 선언할 수 있습니다.

```java
public interface 인터페이스명 { 

}
```

- 인터페이스는 클래스와 마찬가지로 public, default 접근 제어자를 지정할 수 있습니다.

### `2) 인터페이스 구성`

인터페이스의 멤버

- 모든 멤버변수는 public static final 이어야합니다.
  - 생략 가능합니다.
- 모든 메서드는 public abstract 이어야합니다.
  - 생략 가능합니다. (static 메서드와 default 메서드 예외)
- 생략되는 제어자는 컴파일러가 자동으로 추가 해줍니다.

```java
public interface 인터페이스명 { 
        public static final char A = 'A';
    static char B = 'B';
    final char C = 'C';
    char D = 'D';

    void turnOn(); // public abstract void turnOn();
}
```

### `3) 인터페이스 구현`

인터페이스는 추상 클래스와 마찬가지로 직접 인스턴스를 생성할 수 없기 때문에 클래스에 구현되어 생성됩니다.

- implements 키워드를 사용하여 인터페이스를 구현할 수 있습니다.

```java
public class 클래스명 implements 인터페이스명 { 
        // 추상 메서드 오버라이딩
        @Override
    public 리턴타입 메서드이름(매개변수, ...) {
                // 실행문
    }
}
```

- 인터페이스의 추상 메서드는 구현될 때 반드시 오버라이딩 되어야 합니다.
- 만약 인터페이스의 추상 메서드를 일부만 구현해야 한다면 해당 클래스를 추상 클래스로 변경해주면 됩니다.

### `4) 인터페이스 상속`

인터페이스간의 상속이 가능합니다.

- 인터페이스간의 상속은 implements 가 아니라 extends 키워드를 사용합니다.
- 인터페이스는 클래스와는 다르게 다중 상속이 가능합니다.

```java
public class Main implements C {

    @Override
    public void a() {
        System.out.println("A");
    }

    @Override
    public void b() {
                System.out.println("B");
    }
}

interface A {
    void a();
}
interface B {
    void b();
}
interface C extends A, B { }
```

- 인터페이스 C는 아무것도 선언 되어있지 않지만 인터페이스 A, B를 다중 상속받았기 때문에 추상 메서드 a, b를 갖고 있는 상태입니다.
- 따라서 Main 클래스에서 인터페이스 C가 구현될 때 a, b 추상 메서드가 오버라이딩됩니다.
- 또한 인터페이스의 구현은 상속과 함께 사용될 수 있습니다.

```java
public class Main extends D implements C {

    @Override
    public void a() {
        System.out.println("A");
    }

    @Override
    public void b() {
        System.out.println("B");
    }

    @Override
    void d() {
        super.d();
    }

    public static void main(String[] args) {
        Main main = new Main();
        main.a();
        main.b();
        main.d();
    }
}

interface A {
    void a();
}

interface B {
    void b();
}

interface C extends A, B {
}

class D {
    void d() {
        System.out.println("D");
    }
}
```

```java
public class Main extends D implements C {

    @Override
    public void a() {
        System.out.println("A");
    }

    @Override
    public void b() {
        System.out.println("B");
    }

    @Override
    void d() {
        super.d();
    }

    public static void main(String[] args) {
        Main main = new Main();
        main.a();
        main.b();
        main.d();
    }
}

interface A {
    void a();
}

interface B {
    void b();
}

interface C extends A, B {
}

class D {
    void d() {
        System.out.println("D");
    }
}
```

## 02. 디폴트 메서드와 static 메서드

### `1) 디폴트 메서드`

디폴트 메서드는 추상 메서드의 기본적인 구현을 제공하는 메서드입니다.

- 메서드 앞에 default 키워드를 붙이며 블럭{ }이 존재해야합니다.
- default 메서드 역시 접근 제어자가 public 이며 생략이 가능합니다.
- 추상 메서드가 아니기 때문에 인터페이스의 구현체들에서 필수로 재정의 할 필요는 없습니다.

```java
public class Main implements A {

    @Override
    public void a() {
        System.out.println("A");
    }

    public static void main(String[] args) {
        Main main = new Main();
        main.a();

        // 디폴트 메서드 재정의 없이 바로 사용가능합니다.
        main.aa();
    }
}

interface A {
    void a();
    default void aa() {
        System.out.println("AA");
    }
}
```

```java
public class Main implements A {

    @Override
    public void a() {
        System.out.println("A");
    }

    public static void main(String[] args) {
        Main main = new Main();
        main.a();

        // 디폴트 메서드 재정의 없이 바로 사용가능합니다.
        main.aa();
    }
}

interface A {
    void a();
    default void aa() {
        System.out.println("AA");
    }
}
```

### `2) static 메서드`

인터페이스에서 static 메서드 선언이 가능합니다.

- static의 특성 그대로 인터페이스의 static 메서드 또한 객체 없이 호출이 가능합니다.
- 선언하는 방법과 호출하는 방법은 클래스의 static 메서드와 동일합니다.
  - 접근 제어자를 생략하면 컴파일러가 public을 추가해 줍니다.

```java
public class Main implements A {

    @Override
    public void a() {
        System.out.println("A");
    }

    public static void main(String[] args) {
        Main main = new Main();
        main.a();
        main.aa();
        System.out.println();

        // static 메서드 aaa() 호출
        A.aaa();
    }
}

interface A {
    void a();
    default void aa() {
        System.out.println("AA");
    }
    static void aaa() {
        System.out.println("static method");
    }
}
```

```java
public class Main implements A {

    @Override
    public void a() {
        System.out.println("A");
    }

    public static void main(String[] args) {
        Main main = new Main();
        main.a();
        main.aa();
        System.out.println();

        // static 메서드 aaa() 호출
        A.aaa();
    }
}

interface A {
    void a();
    default void aa() {
        System.out.println("AA");
    }
    static void aaa() {
        System.out.println("static method");
    }
}
```

## 03. 다형성

### `1) 타입변환`

예제를 통해 인터페이스의 타입변환은 어떻게 진행이되는지 확인해보겠습니다.

- 자동 타입변환

`인터페이스 변수 = 구현객체;` 는 자동으로 타입 변환이 일어납니다.

```java
public class Main {
    public static void main(String[] args) {
        
        // A 인터페이스에 구현체 B 대입
        A a1 = new B();
        
        // A 인터페이스에 구편체 B를 상속받은 C 대입
        A a2 = new C();
        
    }
}

interface A { }
class B implements A {}
class C extends B {}
```

```java
public class Main {
    public static void main(String[] args) {
        
        // A 인터페이스에 구현체 B 대입
        A a1 = new B();
        
        // A 인터페이스에 구편체 B를 상속받은 C 대입
        A a2 = new C();
        
    }
}

interface A { }
class B implements A {}
class C extends B {}
```

### `2) 강제 타입변환`

`구현객체타입 변수 = (구현객체타입) 인터페이스변수;`

```java
public class Main {
    public static void main(String[] args) {

        // A 인터페이스에 구현체 B 대입
        A a1 = new B();
        a1.a();
        // a1.b(); // 불가능

        System.out.println("\nB 강제 타입변환");
        B b = (B) a1;
        b.a();
        b.b(); // 강제 타입변환으로 사용 가능
        System.out.println();

        // A 인터페이스에 구편체 B를 상속받은 C 대입
        A a2 = new C();
        a2.a();
        //a2.b(); // 불가능
        //a2.c(); // 불가능

        System.out.println("\nC 강제 타입변환");
        C c = (C) a2;
        c.a();
        c.b(); // 강제 타입변환으로 사용 가능
        c.c(); // 강제 타입변환으로 사용 가능

    }
}

interface A {
    void a();
    }
    class B implements A {
    @Override
    public void a() {
        System.out.println("B.a()");
    }

    public void b() {
        System.out.println("B.b()");
    }
    }
    class C extends B {
    public void c() {
        System.out.println("C.c()");
    }
}
```

```java
public class Main {
    public static void main(String[] args) {

        // A 인터페이스에 구현체 B 대입
        A a1 = new B();
        a1.a();
        // a1.b(); // 불가능

        System.out.println("\nB 강제 타입변환");
        B b = (B) a1;
        b.a();
        b.b(); // 강제 타입변환으로 사용 가능
        System.out.println();

        // A 인터페이스에 구편체 B를 상속받은 C 대입
        A a2 = new C();
        a2.a();
        //a2.b(); // 불가능
        //a2.c(); // 불가능

        System.out.println("\nC 강제 타입변환");
        C c = (C) a2;
        c.a();
        c.b(); // 강제 타입변환으로 사용 가능
        c.c(); // 강제 타입변환으로 사용 가능
    

    }
}

interface A {
    void a();
}
class B implements A {
    @Override
    public void a() {
        System.out.println("B.a()");
    }

    public void b() {
        System.out.println("B.b()");
    }
}
class C extends B {
    public void c() {
        System.out.println("C.c()");
    }
}
```

### `4) 인터페이스의 다형성`

인터페이스를 사용하여 다형성을 구현해보겠습니다.

```java
// LG TV 구현체를 조작
MultiRemoteController mrc = new LgTv("LG");
mrc.turnOnOff();
mrc.volumeUp();

// 조작 대상을 Samsung TV로 교체
mrc = new SamsungTv("Samsung");
mrc.turnOnOff();
mrc.channelUp();
```

- `멀티리모컨인터페이스 변수 = TV구현객체;` 를 선언하여 자동 타입변환된 인터페이스 변수를 사용하여 TV구현객체의 기능을 조작할 수 있습니다.

- TV구현객체를 교체해도 멀티리모컨인터페이스 변수는 전혀 수정작업 없이 그대로 기능을 호출할 수 있습니다.

- 다형성은 ‘여러 가지 형태를 가질 수 있는 능력’ 이라고 배웠습니다.

- 사용 방법은 동일하지만 다양한 특징과 결과를 가질 수 있는 것이 바로 다형성입니다.

- 즉, 멀티리모컨으로 티비를 사용하는 방법은 동일하지만 어떤 TV구현객체가 대입되었느냐에 따라 실행 결과가 다르게 나옴을 통해 다형성이 적용되었음을 확인할 수 있었습니다.

```java
// 매개변수와 반환타입 다형성 확인 메서드
default MultiRemoteController getTV(Tv tv) {
    if(tv instanceof SamsungTv) {
    return (SamsungTv) tv;
    } else if(tv instanceof LgTv){
    return (LgTv) tv;
    } else {
    throw new NullPointerException("일치하는 Tv 없음");
    }
}
```

- 또한 인터페이스도 마찬가지로 매개변수와 반환타입에서 다형성이 적용될 수 있습니다.

- 위 예제는 반환타입에는 인터페이스, 매개변수에는 추상클래스로 다형성이 적용되어있습니다.

- 인터페이스의 default 메서드입니다.

- 전체 예제를 통해 더 자세하게 확인해보겠습니다.

```java
public abstract class Tv {

    private String company; // 티비 회사
    private int channel = 1; // 현재 채널 상태
    private int volume = 0;  // 현재 볼륨 상태
    private boolean power = false; // 현재 전원 상태

    public Tv(String company) {
        this.company = company;
    }

    public void displayPower(String company, boolean power) {
        if(power) {
            System.out.println(company + " Tv 전원이 켜졌습니다.");
        } else {
            System.out.println(company + " Tv 전원이 종료되었습니다.");
        }
    }

    public void displayChannel(int channel) {
        System.out.println("현재 채널은 " + channel);
    }

    public void displayVolume(int volume) {
        System.out.println("현재 볼륨은 " + volume);
    }

    public String getCompany() {
        return company;
    }

    public int getChannel() {
        return channel;
    }

    public int getVolume() {
        return volume;
    }

    public boolean isPower() {
        return power;
    }

    public void setChannel(int channel) {
        this.channel = Math.max(channel, 0);
    }

    public void setVolume(int volume) {
        this.volume = Math.max(volume, 0);
    }

    public void setPower(boolean power) {
        this.power = power;
    }
}
```

```java
public class SamsungTv extends Tv implements MultiRemoteController{

    public SamsungTv(String company) {
        super(company);
    }

    @Override
    public void turnOnOff() {
        setPower(!isPower());
        displayPower(getCompany(), isPower());
    }

    @Override
    public void channelUp() {
        setChannel(getChannel() + 1);
        displayChannel(getChannel());
    }

    @Override
    public void channelDown() {
        setChannel(getChannel() - 1);
        displayChannel(getChannel());
    }

    @Override
    public void volumeUp() {
        setVolume(getVolume() + 1);
        displayVolume(getVolume());
    }

    @Override
    public void volumeDown() {
        setVolume(getVolume() - 1);
        displayVolume(getVolume());
    }
}
```

```java
public class LgTv extends Tv implements MultiRemoteController {

    public LgTv(String company) {
        super(company);
    }

    @Override
    public void turnOnOff() {
        setPower(!isPower());
        displayPower(getCompany(), isPower());
    }

    @Override
    public void channelUp() {
        setChannel(getChannel() + 1);
        displayChannel(getChannel());
    }

    @Override
    public void channelDown() {
        setChannel(getChannel() - 1);
        displayChannel(getChannel());
    }

    @Override
    public void volumeUp() {
        setVolume(getVolume() + 1);
        displayVolume(getVolume());
    }

    @Override
    public void volumeDown() {
        setVolume(getVolume() - 1);
        displayVolume(getVolume());
    }
}
```

```java
public interface MultiRemoteController {

    void turnOnOff();
    void channelUp();
    void channelDown();
    void volumeUp();
    void volumeDown();

    // 매개변수와 반환타입 다형성 확인 메서드
    default MultiRemoteController getTV(Tv tv) {
        if(tv instanceof SamsungTv) {
            return (SamsungTv) tv;
        } else if(tv instanceof LgTv){
            return (LgTv) tv;
        } else {
            throw new NullPointerException("일치하는 Tv 없음");
        }
    }

}
```

---

```java
public class Main {
    public static void main(String[] args) {

        // LG TV 구현체를 조작
        MultiRemoteController mrc = new LgTv("LG");
        mrc.turnOnOff();
        mrc.volumeUp();
        mrc.channelDown();
        mrc.channelUp();
        mrc.turnOnOff();

        // 조작 대상을 Samsung TV로 교체
        System.out.println("\n<Samsung TV로 교체>");
        mrc = new SamsungTv("Samsung");
        mrc.turnOnOff();
        mrc.channelUp();
        mrc.volumeDown();
        mrc.volumeUp();
        mrc.turnOnOff();

        // 매개변수, 반환타입 다형성 체크
        System.out.println("\n<매개변수, 반환타입 다형성 체크>");

        MultiRemoteController samsung = mrc.getTV(new SamsungTv("Samsung"));
        samsung.turnOnOff();

        SamsungTv samsungTv = (SamsungTv) samsung;
        samsungTv.turnOnOff();

        System.out.println();
        MultiRemoteController lg = mrc.getTV(new LgTv("LG"));
        lg.turnOnOff();

        LgTv lgTv = (LgTv) lg;
        lgTv.turnOnOff();

    }
}
```
