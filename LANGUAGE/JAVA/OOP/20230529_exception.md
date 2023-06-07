# 객체지향 프로그래밍_예외처리

## 01. 오류 및 예외에 대한 이해

### `1) 프로그램이 직면하는 문제 상황들`

완벽한 프로그램도 제어하지 못하는 문제는 발생한다. 예를들어 특정한 숫자를 입력받아 그 숫자의 두배를 반환하는 아주 간단하지만 완벽해 보이는 프로그램을 개발했다고 해도 문제는 발생할 수 있다.

문제를 `“정의”`하는 것에서 시작한다. 그리고 그 정의가 정교할수록 우리가 `“대응”`할 여지가 많아진다.

우리가 예외상황에 대한 처리를 코드로 미리 해둘 수 있고, 오류가 발생했다면 어떠한 오류와 함께 프로그램이 종료 되었는지를 알게 돼서 해당 오류에 대응 할 수 있다.

숫자가 아닌 입력에는 오류메세지를 띄우고, 오류를 보고 난 이후에는 더 풍부한 메모리를 가진 컴퓨터에서 프로그램을 돌린다면, 조금 더 완벽에 가까운 프로그램이 될 수 있다.

### `2) 오류(Error) vs 예외(Exception)`

문제상황을 구분하기 위해서 사용하는 기준은 일반적으로 `“회복 가능 여부”`이다.
자바에서도 문제 상황에 대한 대응 프로세스를 갖추고 있으며, 자바 역시 문제상황을 오류와 예외로 정의하고 있다.

- `오류(Error)`는 일반적으로 `회복이 불가능한 문제`입니다.

  - 이는 시스템 레벨에서, 또는 주로 환경적인 이유로 발생합니다.

  - 코드의 문제로 발생하는 경우도 있지만, 일단 발생하는경우 일반적으로 회복이 불가능합니다.

  - 에러가 발생한 경우 우리는 어떠한 에러로 프로그램이 종료되었는지를 확인하고 대응합니다.

- `예외(Exception)`는 일반적으로 `회복이 가능한 문제`입니다.

  - 회복이 가능하다는 전제는 우리가 “그 예외가 발생할 수 있다는 것을 인지하고, 대응했을 것 입니다”.

  - 현실적으로 코드레벨에서 할 수 있는 문제상황에 대한 대응은 “예외처리”에 속합니다.

### `3) 예외의 종류`

코드레벨에서 할 수 있는 문제상황에 대한 대응은 “예외처리”인 만큼 예외의 종류를 조금 더 세부적으로 구분할 수 있다.

#### **코드실행 관점에서 예외의 종류**
  
- 컴파일이란?
    프로그래밍 언어라는 특정한 규칙(문법)이 있는 언어를 사용하여 프로그램의 코드를 작성하는 것이고, 그 특정한 규칙이 있기 때문에 컴퓨터(기계)가 이해할 수 있는 코드로 번역한 것

    프로그래밍 언어로 작성한 코드가 컴퓨터가 이해 할 수 있는 언어로 변환되는 것을 **`컴파일`** 이라고 하며, 컴파일 된 코드는 컴퓨터가 이해 할 수 있어서, 실행 시킬수 있는 코드 뭉치인 **`프로그램`** 이라고 합니다.

- 컴파일 에러(예외)

  - .java 파일을 .class 파일로 컴파일할때 발생하는 에러

  - 대부분 자바 프로그래밍 언어의 규칙을 지키지 않았기 때문에 발생

  - 예를들어 있지 않은 클래스를 호출한다거나, 접근이 불가능한 프로퍼티나 메소드에 접근한다거나 하는 경우에 발생

  - 컴파일 에러가 발생하는 경우 해결 방법은 문법에 맞게 다시 작성해야한다.

- 런타임 에러(예외)

  - 우리가 주로 다루게 될 에러(예외)

  - 문법적인 오류는 아니라서, 컴파일은 잘 되었지만 “프로그램”이 실행도중 맞닥뜨리게 되는 예외

#### **예외처리 관점에서 예외**

- 확인된 예외 (Checked Exception)

- 컴파일 시점에 확인하는 예외입니다.

- 반드시 예외 처리를 해줘야하는 예외 입니다.

### ⚠️ **`Checked Exception`** 에 대한 예외처리를 하지 않으면 **`컴파일 에러`** 가 발생

컴파일 시점에 확인하는 예외라는 문구 때문에, 컴파일 에러와 헷갈릴 수 있다.
우리가 이미 특정한 문제를 인지하고 있어서, 해당 예외를 정의해두었고, 정의해두었기 때문에 컴파일 하는동안 이 예외에 대한 예외처리를 했는지 확인(Check) 할 수 있는 예외이다.

- 미확인된 예외🚫 (Unchecked Exception)

- 런타임 시점에 확인되는 예외이다.

- 예외 처리가 반드시 필요하지 않은 예외이다.

## 02. 예외 발생과 try-catch, finally 문

### `1) 예외처리의 흐름 미리보기`

1. 우리가 예외를 어떻게 정의하고,

2. 예외가 발생 할 수 있음을 알리고,

3. 사용자는 예외가 발생 할 수 있음을 알고 예외를 핸들링하는지

### `2) 예외 정의하기`

- 우리는 직접 다음과 같이 우리만의 에러를 정의 할 수 있다.

- 예외 클래스를 만들어 예외를 정의한다.

```java
class OurBadException extends Exception {
    public OurBadException() {
        super("위험한 행동을 하면 예외처리를 꼭 해야합니다!");
    }
}
```

### `3) 클래스를 만들고, 메서드를 만들며 우리의 메서드가 위험하다고 알리기(throw, throws)`

```java
class OurClass {
    private final Boolean just = true;
        
        // 신규 문법 throws!
    public void thisMethodIsDangerous() throws OurException {
        if (just) {
                        // 신규 문법 throw!
            throw new OurException();
        }
    }
}
```

| throws | throw |
| --- | --- |
| 메서드 이름 뒤에 붙어 이 메서드가 어떠한 예외사항을 던질 수 있는지 알려주는 예약어| 메서드 안에서, 실제로 예외 객체를 던질 때 사용하는 예약어 |
| 여러 종류의 예외사항을 적을 수 있다. | 실제로 던지는 예외 객체 하나와 같이 써야한다. |
|  | 일반 메서드의 return 키워드처럼 throw 아래의 구문들은 실행되지 않고, throw문과 함께 메서드가 종료된다. |

우리가 메서드를 선언 할 때, 이 메서드가 위험하다는것을 미리 **예측**해야 한다.
그리고 예측이 되어 있다면, 실제로 throw 키워드와 함께 **이 메서드가 위험하다고 알려야 한다.**

### `4) 위험한 메서드를 사용한다면, 예외를 handling 하기`

```java
public class StudyException {
    public static void main(String[] args) {
        OurClass ourClass = new OurClass();

        try {
            // 1. 위험한 메소드의 실행을 "시도" 해 봅니다.
            // "시도" 해보는 코드가 들어가는 블럭입니다.
            ourClass.thisMethodIsDangerous();
        } catch (OurException e) {
            // 2. 예외가 발생하면, "잡아서" handling 합니다.
            // 예외가 발생하는경우 "handling" 하는 코드가 들어가는 블럭입니다.
                        // 즉 try 블럭 내의 구문을 실행하다가 예외가 발생하면
                        // 예외가 발생한 줄에서 바로 코드 실행을 멈추고
                        // 여기 있는 catch 블럭 내의 코드가 실행됩니다.
            System.out.println(e.getMessage());
        } finally {
            // 3. 예외의 발생 여부와 상관없이, 실행시켜야 하는 코드가 들어갑니다.
            // 무조건 실행되는 코드가 들어가는 블럭입니다.
            System.out.println("우리는 방금 예외를 handling 했습니다!");
        }

    }
}
```

- 위험 감지하기
  
  - 특정한 클래스의 메서드를 사용할 때, 특히 우리가 작성한 코드가 아니라면 더더욱, 이 메서드가 위험한지 알아봐야 한다.
  
  - 보통 메서드의 명세를 확인 할 수 있으며 intellij를 사용중이라면, 커서를 올려 간단하게 확인 할 수 있다.

- 위험을 감지했다면, try-catch(finally) 키워드 이용하기
  
  - `try - catch` 는 각각 중괄호`{}` 를 통해 실행할 코드들을 담는다.
  
  - `try` 단어의 **“시도한다”** 라는 뜻에 맞게 의 중괄호`{}` 안에는 예외가 발생할 수 있지만 실행을 시도할 코드를 담는다.

  - `catch` 단어의 **“잡는다”** 라는 의미에 맞게 중괄호`{}` 안에는 **`try`** 안에있는 코드를 실행하다가 예외가 났을때 실행할 코드를 담는다.

  - `catch` 는 소괄호`()` 를 통해 어떤 예외클래스를 받아서 처리할지 정의해주어야 합니다.
  
  - `catch` 로 모든 예외를 다 받고 싶으면 `Exception` 을 넣어주면 됩니다.
  
  - `catch` 로 일부 예외만 받아서 처리하고 싶으면 해당 예외 클래스명을 넣어주면 됩니다.

  - 1개의 `try` 문에 `catch` 문은 여러개 사용할 수 있습니다. e.g.) 1`try` : 4`catch`
  
  - 기존 `try - catch` 의 맨 마지막에 `finally` 를 붙여서 마지막에 반드시 실행할 코드를 넣을 수 있습니다.

- 예외가 발생하는 상황을 “인지” 했고, 어떠한 에러인지 “정의” 했습니다.

- 메서드를 선언 할 때 예외가 발생하는 위험한 메서드라는 것을 “알렸습니다 (throws/throw)”.

- checked exception을 정의하고, 알렸으니 이 메서드를 사용 할 때 예외처리를 하지 않으면 컴파일 에러가 발생하게된다

## 03. 예외 클래스 구조 이해하기

### `1) 오류 및 예외에 대한 이해 다시보기`

프로그래밍을 하다 보면 “문제” 상황에 직면하고,
맞닥뜨린 문제를 “회복 가능 여부”에 따라 “Error”와, “Exception”으로 나누고,
예외와, 에러를 컴파일/런타임과 같은 여러가지 기준에따라 구체적으로 “정의”한다.

결론적으로 맞닥뜨리는 “문제” 상황을 추상화, 일반화, 구체화 해서 정의한 것이다.

- 가장 추상적인 “문제”
- 그것보다는 조금 더 구체적인 “오류”, “예외”
- 그것보다 더 구체적인 “Checked Exception”, “Unchecked Exception” 과 같이 정의를 할 수 있는 것이다.

자바의 핵심 아이디어이자, 메인 패러다임은 객체 지향 프로그래밍이다.
그것에 맞게 자바의 모든것은 객체로 구현되어 있다.

오류 및 예외에 대한 일반적이고, 추상적인 정의를 가지고 있기 때문에 맞닥뜨리는 “문제”를 추상화해서 객체와 상속관계를 이용해 구현 할 수 있는 것이다.

물론 아직 객체 지향 프로그래밍도, 자바 언어도 익숙하지 않은 우리가 이러한 것들을 직접 구현하는 것은 너무 어렵고 이러한 에러 객체들을 구현하는 것 자체가 언급된 언어 설계 차원에서의 에러 대응 프로세스이기도 하기 때문에 이 문제들을 추상화 해서 객체로 만들어 주는 것은 자바 언어 차원에서 지원해준다.

실제로 어떠한 에러가 어떻게 구현되어 있는지를 공부해서, 더 정확하게 에러 상황을 대응할 지식을 얻는 것 과, 현실에서 마주하는 개념이나 이슈들을 객체지향 프로그래밍으로 어떻게 구현하는지에 대한 좋은 예시를 공부하는 것 이다.

### `2) 자바의 Throwable Class`

- 시작은 모든 객체의 원형인 `Object` 클래스에서 시작한다.
- 앞서 정의한 “문제 상황”을 뜻하는 `Throwable` 클래스가 Object 클래스를 상속하고,
- `Throwable` 클래스의 자식으로 앞서배운 에러(`Error`)와 예외(`Exception`) 클래스가 있다.
- 에러(`Error`) 클래스와 예외(`Exception`) 클래스는 각각 `IOError` 클래스, `RuntimeException` 클래스와 같이 구분하여 처리된다.

참고로 아래 그림의 RuntimeException을 상속한 예외들은 UncheckedException, 반대로 상속하지 않은 예외들은 CheckedException으로 구현되어 있다.

### `3) Exception 클래스 구조`

즉, NullPointException, ArrayIndexOutOfBoundsException 등의 예외 구현체들은 명시적인 에러처리를 하지 않아도 컴파일 에러가 발생하지 않는다.

또 Checked Exception에 속하는 에러 구현체들은 핸들링 하지 않으면 컴파일 에러가 발생하는 대신, 컴파일이 됐다면 100% 복구가 가능한 에러라는 것도 기억해야한다.

### `4) 자바의 수많은 에러 구현체들`

- Java 예외 리스트 (참고용)

```java
// 출처 : https://programming.guide/java/list-of-java-exceptions.html

java.io
IOException
CharConversionException
EOFException
FileNotFoundException
InterruptedIOException
ObjectStreamException
InvalidClassException
InvalidObjectException
NotActiveException
NotSerializableException
OptionalDataException
StreamCorruptedException
WriteAbortedException
SyncFailedException
UnsupportedEncodingException
UTFDataFormatException
UncheckedIOException

java.lang

ReflectiveOperationException
ClassNotFoundException
InstantiationException
IllegalAccessException
InvocationTargetException
NoSuchFieldException
NoSuchMethodException
CloneNotSupportedException
InterruptedException

산술 예외
IndexOutOfBoundsException
ArrayIndexOutOfBoundsException
StringIndexOutOfBoundsException
ArrayStoreException
ClassCastException
EnumConstantNotPresentException
IllegalArgumentException
IllegalThreadStateException
NumberFormatException
IllegalMonitorStateException
IllegalStateException
NegativeArraySizeException
NullPointerException
SecurityException
TypeNotPresentException
UnsupportedOperationException

java.net
HttpRetryException
SocketTimeoutException
MalformedURLException
ProtocolException
SocketException
BindException
ConnectException
NoRouteToHostException
PortUnreachableException
UnknownHostException
UnknownServiceException
URISyntaxException

java.text
ParseException
    

java.time
DateTimeException
    

java.time.zone
ZoneRulesException
```

이미 수많은 구현체들이 있고, 거의 대부분의 상황에 맞는 에러들은 이미 구현되어있다. 명시적으로 어떠한 에러를 내보낼지는 찾아보고 결정하면 된다. 만약 정 찾아봤는데, 없다면 특정 에러를 더 구체화해서 내가 직접 “정의” “구현”하면 된다.

```java

class OurBadException extends Exception {
public OurBadException() {
    super("위험한 행동을 하면 예외처리를 꼭 해야합니다!");
}
}
```

## 4. Chained Exception, 실제 예외 처리하는 방법

- 연결된 예외 (Chained Exception)

- 예외는 다른 예외를 유발할 수 있습니다.

- 예외 A가 예외 B를 발생시켰다면, 예외 A는 B의 원인 예외입니다.

- 원인 예외를 새로운 예외에 등록한 후 다시 새로운 예외를 발생시키는데,
이를 **예외 연결**이라고 합니다.

    👉 왜 예외를 연결하죠?

- 예외를 연결하는 이유는 여러 가지 예외를 하나의 큰 분류의 예외로 묶어서 다루기 위함

- checked exception을 unchecked exception으로 포장(wrapping)하는데 유용하게 사용되기도 한다.

### `1) 원인 예외를 다루기 위한 메소드`

- **`initCause()`**

  - 지정한 예외를 원인 예외로 등록하는 메소드

- **`getCause()`**

  - 원인 예외를 반환하는 메소드

```java
// 연결된 예외 
public class main {

    public static void main(String[] args) {
        try {
            // 예외 생성
            NumberFormatException ex = new NumberFormatException("가짜 예외이유");

            // 원인 예외 설정(지정한 예외를 원인 예외로 등록)
            ex.initCause(new NullPointerException("진짜 예외이유"));

            // 예외를 직접 던집니다.
            throw ex;
        } catch (NumberFormatException ex) {
            // 예외 로그 출력
            ex.printStackTrace();
            // 예외 원인 조회 후 출력
            ex.getCause().printStackTrace();
        }

        // checked exception 을 감싸서 unchecked exception 안에 넣습니다.
        throw new RuntimeException(new Exception("이것이 진짜 예외 이유 입니다."));
    }
}

// 출력
Caused by: java.lang.NullPointerException: 진짜 예외이유
```

### `2) 실제로 예외 처리하기`

실질적으로 예외를 처리하는 방법으로는 예외 복구, 예외 처리 회피, 예외 전환 이 있습니다.

#### 1. 예외 복구하기

```java
public String getDataFromAnotherServer(String dataPath) {
        try {
                return anotherServerClient.getData(dataPath).toString();
        } catch (GetDataException e) {
                return defaultData;
        }
}
```

- 실제로 try-catch로 예외를 처리하고 프로그램을 정상 상태로 복구하는 방법입니다.

- 가장 기본적인 방식이지만, 현실적으로 복구가 가능한 상황이 아닌 경우가 많거나 최소한의 대응만 가능한 경우가 많기 때문에 자주 사용되지는 않습니다.

#### 2. 예외 처리 회피하기

```java
public void someMethod() throws Exception { ... }

public void someIrresponsibleMethod() throws Exception {
        this.someMethod();
}
```

- 이렇게 처리하면, someMethod()에서 발생한 에러가 someIrresponsibleMethod()의 throws를 통해서 그대로 다시 흘러나가게 되겠죠, 물론 같은 객체내에서 이런일은 하지는 않습니다, 예외처리 회피를 보여드리기 위한 단순한 예시 코드입니다.

- 관심사를 분리해서 한 레이어에서 처리하기 위해서 이렇게 에러를 회피해서 그대로 흘러 보내는 경우도 있습니다.

#### 3. 예외 전환하기

```java
public void someMethod() throws IOException { ... }

public void someResponsibleMethod() throws MoreSpecificException {
        try {
            this.someMethod();
        } catch (IOException e) {
            throw new MoreSpecificException(e.getMessage());
        }
}
```

- 예외처리 회피하기의 방법과 비슷하지만, 조금더 적절한 예외를 던져주는 경우 입니다.

- 보통은 예외처리에 더 신경쓰고싶은 경우나, 오히려 RuntimeException처럼 일괄적으로 처리하기 편한 예외로 바꿔서 던지고 싶은 경우 사용합니다.
