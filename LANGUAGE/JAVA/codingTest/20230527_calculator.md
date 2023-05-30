# HW . Interface

## **계산기 만들기**

- Step 1
    더하기, 빼기, 나누기, 곱하기 연산을 수행할 수 있는 Calculator 클래스를 만듭니다.
  
  - Calulator 클래스는 연산을 수행하는 반환타입이 double 인 calculate 메서드를 가지고 있습니다.
  - calculate 메서드는 String 타입의 operator 매개변수를 통해 연산자 매개값을 받습니다.
  - int 타입의 firstNumber, secondNumber 매개변수를 통해 피연산자 값을 받습니다.
  - calculate 메서드는 전달받은 피연산자, 연산자를 사용하여 연산을 수행합니다.
  
- Step 2
    나머지 연산자(%)를 수행할 수 있게 Calculator 클래스 내부코드를 변경합니다.
- Step 3
    AddOperation(더하기), SubstractOperation(빼기), MultiplyOperation(곱하기), DivideOperation(나누기) 연산 클래스를을 만든 후 클래스간의 관계를 고려하여 Calculator 클래스와 관계를 맺습니다.
  
- 관계를 맺은 후 필요하다면 Calculator 클래스의 내부코드를 변경합니다.
  - 나머지 연산자(%) 기능은 제외합니다.
- Step 2 와 비교하여 어떠한 점이 개선 되었는지 스스로 생각해 봅니다.
  - 단일 책임 원칙 `SRP` (Single Responsibility Principle)
  객체는 `단 하나의 책임만 가져야 한다`는 원칙을 말한다.

  여기서 '책임' 이라는 의미는 하나의 '기능 담당'으로 보면 된다.

  하나의 클래스에 여러 기능(책임)을 넣느냐, 따로따로 클래스를 분리하여 기능(책임)을 분산시키느냐 설계는 프로그램의 유지보수와 밀접한 관련이 있다.

  단일 책임 원칙 준수 유무에 따른 가장 큰 특징 기준 척도는, '기능 변경(수정)' 이 일어났을때의 파급 효과 이다.

  한 객체에 책임이 많아질수록 클래스 내부에서 서로 다른 역할을 수행하는 코드끼리 강하게 결합될 가능성이 높아지게 되어 시스템이 복잡해질 수 있다. 그래서 그 객체가 하는 기능에 변경사항이 생기면 이 기능을 사용하는 부분의 코드를 모두 다시 테스트를 해야 할 수도 있다.

  예를 들어 A를 고쳤더니 B를 수정해야하고 또 C를 수정해야하고, C를 수정했더니 다시 A로 돌아가서 수정해야 하는, 마치 책임이 순환되는 형태를 들 수 있다.

  이 처럼 책임이 이것저것 포함된 클래스는 한 책임의 변경에서 다른 책임의 변경으로의 연쇄작용이 일어 나게 된다.

  여기서 단일 책임 원칙을 적용한다면, 각 클래스 주제마다 알맞는 책임을 가짐으로서 책임 영역이 확실해지게 된다.

  그래서 어떠한 역할에 대해 변경사항이 발생했을때, 변경 영향을 받는 기능만 모아둔 클래스라면 그 책임을 지니고 있는 클래스만 수정해주면 될 일이다.

  이것을 다르게 말하면, 모듈이 변경되는 이유가 한가지 여야 함을 뜻한다. 여러가지 책임을 가지고 있으면 각기 다른 사유에 의해서 모듈이 변경되는 이유가 여러가지가 되기 때문이다.
  
- Step 4
    AddOperation(더하기), SubstractOperation(빼기), MultiplyOperation(곱하기), DivideOperation(나누기) 연산 클래스들을 AbstractOperation(추상 클래스)를 사용하여 추상화하고 Calculator 클래스의 내부 코드를 변경합니다.

- Step 3 와 비교해서 어떠한 점이 개선 되었는지 스스로 생각해 봅니다.
  - 객체지향의 5대 원칙 중, 의존성 역전 원칙(`DIP`) Dependency Injectoin Principle 이란 "추상화에 의존해야지, 구체화에 의존하면 안 된다" 는 원칙입니다.

  - 고수준 모듈 : 어떤 의미 있는 단일 기능을 제공하는 모듈 (interface, 추상 클래스)
  - 저수준 모듈 : 고수준 모듈의 기능을 구현하기 위해 필요한 하위 기능의 실제 구현 (메인클래스, 객체)

  고수준 모듈은 저수준 모듈의 구현에 의존해서는 안 됩니다.
  대신 저수준 모듈이 고수준 모듈에서 정의한 추상 타입에 의존해야 합니다. 사실 고수준 클래스가 저수준 클래스를 사용하므로 고수준 클래스가 저수준 클래스에 의존하는 것이 자연스러워 보일 수 있습니다. 하지만 저수준 클래스는 빈번하게 변경되고, 새로운 것이 추가될 때마다 고수준 클래스가 영향을 받기 쉬우므로 의존관계를 역전시켜야 합니다.

  DIP를 만족하면, `의존성 주입(DI)`이라는 기술로 변화를 쉽게 수용할 수 있는 코드를 작성할 수 있습니다.

### 🔑힌트

- Step 1
  - if or switch 즉, 제어문을 통해 연산자의 타입을 확인하고 해당하는 타입의 연산을 수행하고 결과값을 반환합니다.
- Step 2
  - 제어문에 나머지 연산자(%)를 추가합니다.
- Step 3
  - AddOperation, SubstractOperation, MultiplyOperation, DivideOperation 연산 클래스들을 만듭니다.
  - 각각의 연산타입에 맞게 operate 메서드를 구현합니다.
  - Calculator 클래스와 포함관계를 맺고 생성자를 통해 각각의 연산 클래스 타입의 필드에 객체를 주입합니다.
  - calculate 메서드에서 직접 연산을 하지 않고 주입 받은 연산 클래스들의 operate 메서드를 사용하여 연산을 진행합니다.
- Step 4
  - AbstractOperation 추상 클래스를 만들고 operate 추상 메서드를 만듭니다.
  - AddOperation, SubstractOperation, MultiplyOperation, DivideOperation 클래스들은 AbstractOperation 클래스를 상속받고 각각의 연산타입에 맞게 operate를 오버라이딩 합니다.
  - Calculator 클래스는 4개의 연산 클래스들이 상속받고 있는 AbstractOperation 클래스만을 포함합니다.
  - 생성자 혹은 Setter를 사용하여 연산을 수행할 연산 클래스의 객체를 AbstractOperation 클래스 타입의 필드에 주입합니다.(다형성)
  - calculate 메서드에서는 더 이상 연산자 타입을 받아 구분할 필요없이 주입 받은 연산 클래스의 operate 메서드를 통해 바로 연산을 수행합니다.

![계산기](/assets/3%EC%A3%BC%EC%B0%A8%EA%B3%84%EC%82%B0%EA%B8%B0.PNG)
나누기 연산이 0.0만 출력되는게 아니였다..
![계산기2](/assets/3%EC%A3%BC%EC%B0%A8%EA%B3%84%EC%82%B0%EA%B8%B02.PNG)
소수 이하가 연산이 안되는거였다..

### 객체지향의 5대 원칙 `SOLID`

- 단일 책임 원칙 (Single Responsibility principle)
- 개방 폐쇄 원칙 (Open Closed Principle)
- 리스코프 치환 원칙 (Liscov Substitution Principle)
- 인터페이스 분리 원칙 (Interface Sergregation Principle)
- 의존성 역전 원칙 (Dependency Inversion Principle)
