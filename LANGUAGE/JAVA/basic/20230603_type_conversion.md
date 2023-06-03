# **Type Conversion** 형 변환

형식이 다른 데이터들을 더하려면 한쪽의 데이터 타입을 다른 쪽의 데이터 타입으로 전환(Conversion)해야 한다. 자바는 이러한 형 변환을 자동으로 처리해주는데 이러한 전환작업을 자동(암시적) `형 변환(implicit Conversion)`이라고 부른다.
자동 형 변환이 적용되지 않는 경우에는 수동으로 형 변환을 해야 한다. 이를 `명시적` 또는 `묵시적(Explicit Conversion) 형 변환`이라고 한다.

자동 형 변환의 원칙은 표현범위가 좁은 데이터 타입에서 넓은 데이터 타입으로의 변환만 허용된다는 것이다.

## 1. 정수형, 실수형 간 발생하는 형변환

정수 ↔ 실수 간에 변환할때는 `({원하는 타입})` 명령을 통해 변환할 수 있다. (캐스팅)

- **Double, Float to Int**
  
  (Int)캐스팅 방식으로 실수를 정수로 치환하는 방법이다.
  
  이때 실수형의 소수점아래자리는 버려집니다.
  
```java
double doubleNumber = 10.101010;
float floatNumber = 10.1010

int intNumber;
intNumber = (int)doubleNumber; // double -> int 형변환
intNumber = (int)floatNumber; // float -> int 형변환
```
  
- **Int to Double, Float**
  
  (Double,Float) 캐스팅으로 정수형을 실수형으로 변환하는 방법이다.
  
```java
int intNumber = 10;

double doubleNumber = (double)intNumber; // int -> double 형변환
float floatNumber = (float)intNumber;  // int -> float 형변환
```

- 자동 형변환
  - Java 프로그래밍에서 형변환을 직접적으로 캐스팅하지 않아도 자동으로 형변환 되는 케이스가 있다.
  - 프로그램 실행 도중에 값을 저장하거나 계산할때 자동으로 타입변환이 일어난다.

### 1) 자동 타입변환은 작은 크기의 타입에서 큰 크기의 타입으로 저장될때 큰 크기로 형변환이 발생한다

📌 **변수 타입별 크기 순서**
byte(1) → short(2) → int(4) → long(8) → float(4) → double(8)

```java
byte byteNumber = 10;
int intNumber = byteNumber;    // byte -> int 형변환
System.out.println(intNumber); // 10

char charAlphabet = 'A';
intNumber = charAlphabet;   // char -> int 형변환
System.out.println(intNumber); // A의 유니코드 : 65

intNumber = 100;
long longNumber = intNumber; // int -> number 형변환
System.out.println(longNumber); // 100

intNumber = 200;
double doubleNumber = intNumber; // int -> double 형변환
System.out.println(doubleNumber); // 200.0  (소수점이 추가된 실수출력)
```

### 2) 작은 크기의 타입이 큰 크기의 타입과 계산될때 자동으로 큰 크기의 타입으로 형변환이 발생한다

```java
int intNumber = 10;
double doubleNumber = 5.5;
double result = intNumber + doubleNumber; // result 에 15.5 저장됨 (int -> double)

intNumber = 10;
int iResult = intNumber / 4; // iResult 에 2 저장됨 (int형 연산 -> 소수점 버려짐)

intNumber = 10;
double dResult = intNumber / 4.0; // dResult 에 2.5 저장됨 (double형 연산 -> 소수점 저장)
```

### **🔥 정리**

자동 형변환 vs 강제 형변환

- `**작은 타입` > `큰 타입` 형변환시 **(자동 형변환)**
  - 더 큰 표현범위를 가진 타입으로 변환되는것이라 값의 손실이 없다.
  - 값의 손실없이 변환이 가능하기 때문에 컴파일러가 자동으로 형변환을 해준다.
- `**큰 타입` > `작은 타입` 형변환시 **(강제 형변환 = 캐스팅)**
  - 더 작은 표현범위를 가진 타입으로 변환된는것이라 값의 손실이 생긴다.
  - 값의 손실이 생기기 때문에 자동으로 형변환을 해주지 않고 개발자가 선택하여 형변환을 한다.

`byte` 타입은 `short`가 될 수 있지만 `short`는 `byte` 타입이 될 수 없다.
`long`은 `float`가 될 수 있지만, `float`는 `long`이 될 수 없다.
