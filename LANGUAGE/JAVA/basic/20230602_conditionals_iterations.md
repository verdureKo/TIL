# **Iterations & Conditionals** 반복문과 조건문

컴퓨터는 이런 반복적인 작업을 대행하기 위해서 만들어진 기계다.
인간이 하기 싫어하는 바로 그 일을 컴퓨터가 대신하도록 하는 것이 반복문(loop, iteration)이다.

## 1. 반복문의 문법

반복문의 문법은 몇 가지가 있다.
각각의 구문은 서로 대체 가능하기 때문에 상황과 취향에 따라서 선택해서 사용하면 된다.

### **1) while문**

```java
while(조건){
    반복 실행 영역
}
```

다음 예제는 무한 반복을 발생시킨다.
저장되지 않은 작업이 있다면 모두 정리한 후에 이 명령을 실행하자.
콘솔에서 실행할 경우 Ctrl+C(dnls 나 Cmd+.) 단축키를 이용해서 무한 반복을 중지할 수 있다.

```java
public class WhileDemo {
 
    public static void main(String[] args) {
        while (true) {
            System.out.println("Coding Everybody");
        }
    }
}
```

이번에는 true를 false로 바꾼 아래의 예제를 실행해보자.
아래 코드는 아예 컴파일조차 되지 않을 것이다.
반복 조건이 false이기 때문에 반복문이 한 번도 실행되지 않을 것이기 때문에 컴파일러가 오류를 발생시키는 것이다.

```java
while(false){
    System.out.println("Coding Everybody");
}
```

while 문은 `반복조건이 참(true)이면 중괄호 구간을 반복적으로 실행`한다.
조건이 false면 반복문이 실행되지 않는다.

여기서 true와 false는 반복의 종료조건이 되는데, 반복문에서 종료조건을 잘못 지정하면 무한 반복이 되거나, 반복문이 실행되지 않는다.

아래의 반복문은 i의 값을 1씩 순차적으로 증가시킴으로써 반복의 지속 여부를 결정하고 있다. 변수 i는 관습적으로 반복의 조건으로 사용하는 임의의 변수다. 변수이름은 다른것을 사용해도 됨

```java
int i = 0;
// i의 값이 10보다 작다면 true, 크다면 false가 된다. 현재 i의 값은 0이기 때문에 이 반복문은 실행된다. 
while(i<10){         
    System.out.println("Coding Everybody"+i);
    // i의 값에 1을 더한다. 반복문의 중괄호의 마지막 라인에 도달하면 반복문은 반복문을 재호출한다. 이때 i<10의 값을 검사하게 된다.
    i++;
}
```

### **2) for문**

```java
for(초기화; 종료조건; 반복실행){
    반복적으로 실행될 구문
}
```

`while문`을 보면 `반복의 횟수를 지정하기 위해`서 while문 `외부에 변수 i의 값을 초기화`하고, `while문 안에서 i의 값을 증가`시키고 있다. 이것은 `코드를 산만하게 할 수 있다.` 반복문에서 자주 사용하는 `이러한 패턴을 문법적인 형태로 만든 것이 for문`이다. for문은 `특정한 횟수만큼 반복 실행`을 하는 경우에 자주 사용된다. 하지만 for문이나 while문이나 서로 대체 가능하다.
while과 for의 관계는 조건문으로 비유해서 생각해 볼 수도 있을 것 같다.

```java
public class ForDemo {
 
    public static void main(String[] args) {
        for (int i = 0; i < 10; i++) {
            System.out.println("Coding Everybody " + i);
        }
    }
}
```

for문의 괄호 안에는 반복의 종료 조건이 들어온다.

종료 조건은 크게 3개의 부품으로 구성되는데 아래와 같다.

- 초기화 : 반복문이 실행될 때 1회 실행된다.
- 종료조건 : 초기화가 실행된 후에 종료조건이 실행된다. 종료조건의 값이 false일 때까지  반복문의 중괄호 구간의 코드가 반복 실행된다.
- 중괄호 구간의 실행이 끝나면 반복 실행이 실행된다. 일반적으로 이 곳에 i++와 같이 변수를 증가시키는 로직이 위치하고, 이것이 실행된 후에 종료조건이 실행된다. 종료조건이 false가 될 때까지 이 과정이 반복된다.

#### 예시

```java
System.out.println("coding everybody1");
System.out.println("coding everybody2");
System.out.println("coding everybody3");
System.out.println("coding everybody4");
System.out.println("coding everybody5");
System.out.println("coding everybody6");
System.out.println("coding everybody7");
System.out.println("coding everybody8");
System.out.println("coding everybody9");
System.out.println("coding everybody10");
```

```java
int i = 0;
while(i<10){
    System.out.println("coding everybody" + i);
    i++;
}
```

```java
for (int i = 0; i < 10; i++) {
    System.out.println("Coding Everybody " + i);
}
```

coding everybody 뒤에 붙는 숫자를 2의 배수하고 싶다면 어떻게 해야 할까? 반복문이 없다면 한줄 한줄 수정해야 할 것이다. 반복문에서는 내용을 조금만 변경하면 된다.

```java
int i = 1;
while(i<11){
    System.out.println("coding everybody"+(i+1)*2);
    i++;
}
```

```java
for (int i = 1; i < 11; i++) {
    System.out.println("Coding Everybody "+(i+1)*2);
}
```

### **3) 향상된 for문**

- for 소괄호 안에 값이 3개나 들어가기 때문에 이걸 2개로 줄여주는 방법이 향상된 for문이다.
- 향상된 for 문은 연속된 변수목록을 출력할때 쓰인다.
- `for` (`변수 타입` `변수 명` : `목록변수`)  `{ (연산) }` 형태로 사용한다.
- `변수 타입` 과 `변수 명` 은 for 문안에서 연산을 수행할 변수를 정의한다.
- `목록변수`는 3,6,9,12,15 처럼 값여러개를 하나의 변수로 저장하고 싶을때 사용한다.

📌 목록변수는 “배열”이라고 부른다. 배열에 관한 것은 따로 정리하도록 하겠다.

```java
// 향상된 for 문

int[] numbers = {3,6,9,12,15};
for(int number: numbers) {
    System.out.print(number + " "); 
}

// 출력
3 6 9 12 15
```

```java
// 만약 기존 for 문으로 구현한다면?

int[] numbers = {3,6,9,12,15};
for(int i = 0; i < numbers.length; i++) { // 배열에 .length 를 붙이면 길이값이 응답됩니다.
    System.out.println(numbers[i]);
}

// 출력
3 6 9 12 15
```

### **break**

반복작업을 중간에 중단시키고 싶다면 break를 사용하면 된다.
2행의 if(i == 5) 에 의해서 i의 값이 5일 때 break 문이 실행되면서 반복문이 완전히 종료된다.

```java
public class BreakDemo {
 
    public static void main(String[] args) {
        for (int i = 0; i < 10; i++) {
            if (i == 5)
                break;
            System.out.println("Coding Everybody " + i);
        }
    }
}
```

### **continue**

실행을 즉시 중단하면서 반복은 지속해가게 하려면 continue문을 사용하면 되는데, 해당 구문은 이 명령이 나타나는 이후의 로직을 실행하지 않도록 한다. 하지만 반복문 자체를 중단하는 것이 아니고 다시 반복문이 실행되기 때문에 결과는 i가 5가 되었을때의 결과만 출력되지않고 실행이 반복된다.

```java
public class BreakDemo {
 
    public static void main(String[] args) {
        for (int i = 0; i < 10; i++) {
            if (i == 5)
                break;
            System.out.println("Coding Everybody " + i);
        }
    }
}
```

### 반복문의 중첩

반복문 안에는 다시 반복문이 나타날 수 있다.

```java
public class LoopDepthDemo {
 
    public static void main(String[] args) {
        for (int i = 0; i < 10; i++) {
            for (int j = 0; j < 10; j++) {
                System.out.println(i + "" + j);
            }
        }
    }
}
```

이런 경우엔 안쪽의 구문이 먼저 수행되고 외부 구문이 수행된다.

### **4) do-while문**

```java
// do-while 문

int number = 4;
do {
    System.out.println(number + "출력"); 
} while(number < 3); // 연산을 한번 수행 후 조건문 체크

// 출력
```

- `do { (연산) }` `while(조건문)` 형태로도 사용합니다. (do-while 문)
- 위처럼 do-while 문으로 사용하면 최초 1회 연산수행 후 조건문을 체크하여 더 반복할지 결정합니다.
- 반복하게 된다면 그 이후에는 한번 반복할때마다 조건문을 체크해서 조건문이 불만족(false) 이면 반복을 중단합니다.

## 2. 조건문

### **1) if문**

- 특정 조건에 따라 다른 연산을 수행하고 싶을때 사용하는 문맥입니다.
- 기본적인 조건에 따른 연산을 수행하기 위해 `if(조건)` `{ 연산 }` 형태로 사용합니다.
- `if` 의 소괄호() 안의 조건이 boolean 값 true 를 만족하면 중괄호 {} 안의 연산을 수행합니다.

```java
// 조건문
boolean flag = true;

if (flag) {
    System.out.println("flag 값은 true 입니다."); // flag 값은 true 입니다. 출력
}
```

### **2) if-else if문**

- `if문` 조건이 거짓일 경우에 다시한번 다른조건으로 체크해서 참일 경우에 연산을 수행하기 위해  `else if(조건) { 연산 }` 형태로 사용합니다.
- `else if` 의 소괄호() 안의 조건이 boolean 값 true 를 만족하면 `else if` 의 중괄호 {} 안의 연산을 수행합니다.

```java
// 조건문 with else if
int number = 2;

if (number == 1) {
    System.out.println("number 값은 1 입니다."); // 미출력
} else if (number == 2) {
    System.out.println("number 값은 2 입니다."); // number 값은 2 입니다. 출력
} else {
    System.out.println("number 값은 모르는 값입니다."); // 미출력
}
```

### **중첩 if조건**

- `if 문`에 `else`, `else if` 로 해결할 수 없는 복잡한 조건이 있을 수 있습니다.
- 이럴때 중첩해서 `if 문` 또는 `else if문` 또는 `else 문` 안에 `if 문`을 넣을 수 있습니다.

```java
// 중첩 조건문
boolean flag = true;
int number = 2;

if (flag) {
    if (number == 1) {
         System.out.println("flag 값은 true, number 값은 1 입니다."); // 미출력
  } else if (number == 2) {
     System.out.println("flag 값은 true, number 값은 2 입니다."); // flag 값은 true, number 값은 2 입니다. 출력
    }
} else {
    if (number == 1) {
        System.out.println("flag 값은 false, number 값은 1 입니다."); // 미출력
  } else if (number == 2) {
        System.out.println("flag 값은 false, number 값은 2 입니다."); // 미출력
    }
}
```

### **2) switch문**

switch 문은 case 문과 함께 사용하며 if문 보다 좀더 가독성이 좋은 조건문 표현식 입니다.

- `switch(피연산자)` `{ case(조건): (연산) }` 이러한 형태로 많이 쓰입니다.
- `switch 피연산자`가 `case 조건`을 만족하면 `case:` 뒤에 명시되어 있는 연산을 수행합니다.
- `case(조건): (연산)` 은 여러개를 설정할 수 있습니다.
- 🔎 각 case 의 연산문 마지막에는 `break;` 를 꼭 넣어줘야 합니다!!
- `break;` 문은 해당 case 의 연산문이 끝났다는것을 알려주어 switch 문을 종료시켜줍니다.

만약 case 의 연산문 마지막에 `break;` 를 안넣어주면 어떻게 될까요?

- case 의 연산문이 안끝났기때문에 `switch` 문 블럭이 끝날때 까지 전부 실행됩니다!
- `switch문` 중괄호 안의 제일 마지막에 `default: (연산)` 을 명시해주어 `case 조건`들이 모두 만족하지 않을때 수행할 연산을 정해주어야 합니다.
- `default: (연산)` 은 아무것도 만족하지 않을때 수행하는 것이라, 없다면 생략해도 됩니다.

```java
// switch/case 문 

int month = 8;
String monthString = "";
switch (month) {
    case 1:  monthString = "1월";
             break;
    case 2:  monthString = "2월";
             break;
    case 3:  monthString = "3월";
             break;
    case 4:  monthString = "4월";
             break;
    case 5:  monthString = "5월";
             break;
    case 6:  monthString = "6월";
             break;
    case 7:  monthString = "7월";
             break;
    case 8:  monthString = "8월"; 
             break;
    case 9:  monthString = "9월";
             break;
    case 10: monthString = "10월";
             break;
    case 11: monthString = "11월";
             break;
    case 12: monthString = "12월";
             break;
    default: monthString = "알수 없음";
}
System.out.println(monthString); // 8월 출력
```

- if 문과 switch 문
👀 우리가 배운 if 문과 switch 문 모두 조건문을 구현하는 문맥💌 입니다.

그렇다면 둘이 어떻게 다른지 비교를 해볼까요?

- 차이점
    1. 복합조건
        - if 문은 복합조건을 지원합니다.
        - 복합조건 : 괄호`()`안에 조건 여러개를 지정하여 조건문을 수행할 수 있습니다.
        - switch 문은 피연산자 한개에 대한 조건만 지원합니다.
- 차이점
    2. 코드중복
        - if 문은 상대적으로 코드중복이 많습니다.
        - switch 문은 코드중복이 적습니다.

```java
// if vs switch
// switch 문 실습코드를 if 문으로 바꿔보겠습니다.

// switch 
int month = 8;
String monthString = "";
switch (month) {
    case 1:  monthString = "1월";
             break;
    case 2:  monthString = "2월";
             break;
    case 3:  monthString = "3월";
             break;
    case 4:  monthString = "4월";
             break;
    case 5:  monthString = "5월";
             break;
    case 6:  monthString = "6월";
             break;
    case 7:  monthString = "7월";
             break;
    case 8:  monthString = "8월"; 
             break;
    case 9:  monthString = "9월";
             break;
    case 10: monthString = "10월";
             break;
    case 11: monthString = "11월";
             break;
    case 12: monthString = "12월";
             break;
    default: monthString = "알수 없음";
}
System.out.println(monthString); // 8월 출력

// if 로 변환
if (month == 1) {
    monthString = "1월";
} else if (month == 2) {
    monthString = "2월";
} else if (month == 3) {
    monthString = "3월";
} else if (month == 4) {
    monthString = "4월";
} else if (month == 5) {
    monthString = "5월";
} else if (month == 6) {
    monthString = "6월";
} else if (month == 7) {
    monthString = "7월";
} else if (month == 8) {
    monthString = "8월";
} else if (month == 9) {
    monthString = "9월";
} else if (month == 10) {
    monthString = "10월";
} else if (month == 11) {
    monthString = "11월";
} else if (month == 12) {
    monthString = "12월";
} else {
    monthString = "알수 없음";
}
System.out.println(monthString); // 8월 출력
```
