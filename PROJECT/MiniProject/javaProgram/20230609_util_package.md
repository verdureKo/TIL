# 호텔 예약 프로그램_02

음.. 다들 문제없이 마무리 해버리셔서 과제가 빨리끝나는 바람에 선택사항을 구현하게 되었다.
나는 UUID클래스 역시 몰랐기때문에 먼저 보고 정규표현식에 대해 정리해보겠다.

## UUID

import java.util.UUID;
이렇게 자바 유틸패키지에서 UUID 클래스를 임포트해주면 사용할 수 있다.

```java
public class Reservation {

  // 객실, 고객 이름, 고객 전화번호, 예약 날짜, uuid
  private Room room;
  private String customerName, phoneNumber, reservationDate, id;

  public Room getRoom() {
      return room;
  }

  public String getCustomerName() {
      return customerName;
  }

  public String getPhoneNumber() {
      return phoneNumber;
  }

  public String getReservationDate() {
      return reservationDate;
  }

  public String getId() {
      return id;
  }

  public Reservation(Room room, String customerName, String phoneNumber, String reservationDate) {
      this.room = room;
      this.customerName = customerName;
      this.phoneNumber = phoneNumber;
      this.reservationDate = reservationDate;
      this.id = UUID.randomUUID().toString();
  }
}
```

Reservation클래스에 예약시 랜덤번호로 발급되는 고유번호 필드로 사용하였다.

## 정규표현식 (Regular Expression)

정규 표현식은 특정한 규칙을 가진 문자열의 패턴을 표현하는데 사용하는 표현식(Expression)으로 텍스트에서 특정 문자열을 검색하거나 치환할 때 흔히 사용된다. 예를 들어, 웹페이지에서 전화번호나 이메일 주소를 발췌한다거나 로그파일에서 특정 에러메시지가 들어간 라인들을 찾을 때 정규 표현식을 사용하면 쉽게 구현할 수 있다. 정규 표현식은 간단히 정규식, Regex 등으로 불리기도 한다.


import java.util.regex.Pattern;
앞서 설명한 방법과 같이 자바유틸 패키지에서 필요한 클래스를 임포트하면 사용할 수 있다.

호텔예약 프로그램에 사용한 클래스는 Pattern과 Matcher 클래스이다.

### **Pattern 클래스**

```java
public String showRoomList() {
      System.out.println("\n------ 객실 목록 ------");
      String resDate = null;
      LocalDate today = LocalDate.now();
      // 오늘 날짜 출력(iso 8601에 따라 표현된 날짜)
      System.out.println("오늘은 " + LocalDate.now() + " 입니다.");
      // 고객으로부터 원하는 날짜 입력받기
      Scanner scan = new Scanner(System.in);
      //yyyy년 MM월 dd일 타입으로 입력받기
      String pattern = "\\d{4}-(0[1-9]|1[012])-(0[1-9]|[12][0-9]|3[01])";
      while (true) {
          System.out.println("yyyy-MM-dd 형태로 원하시는 날짜를 입력해주세요. 예: 2023-06-05 ");
          resDate = scan.nextLine();
          if (Pattern.matches(pattern, resDate)) { //날짜 형식 체크
              LocalDate reservationDate = LocalDate.parse(resDate);
              int compare = reservationDate.compareTo(today);
              if (compare < 0) {
                  System.out.println("오늘 이전의 날은 입력하실 수 없습니다.");
                  continue;
              }
              System.out.printf("%-13s | %s\n", "방 이름", "가격(만원)");
              for (Room room : roomList) {
                  if (!room.getDateList().contains(resDate)) {
                      System.out.printf("%-15s | %.1f\n", room.getRoomSize(), room.getRoomCharge());
                  }
              }
              break;
          }
          System.out.println("날짜 형식이 올바르지 않습니다.");
      }
      return resDate;
  }

      private String InputPhoneCheck() { //전화번호 정규표현식
        Scanner scan = new Scanner(System.in);
        String pattern = "^01(?:0|1|[6-9])-(?:\\d{3}|\\d{4})-\\d{4}$"; // 숫자만 등장하는지
        while (true) {
            System.out.print("전화번호를 입력해주세요 ex)000-0000-0000 : ");
            String inputPhone = scan.nextLine();
            if (Pattern.matches(pattern, inputPhone))
                return inputPhone;
            System.out.println("올바른 전화번호 형식이 아닙니다. 다시 입력해주세요");
        }
    } // InputPhoneCheck()
```

정규 표현식에 대상 문자열을 검증하는 기능은 java.util.regex.Pattern 클래스의 matches()메소드를 활용하여 검증할 수 있다. matches() 메서드의 첫번째 매개값은 정규표현식이고 두번째 매개값은 검증 대상 문자열이다. 검증 후 대상문자열이 정규표현식과 일치하면 true, 그렇지 않다면 false값을 리턴한다.

날짜와 전화번호를 입력받을때 이를 사용하였다.

## 자주 사용하는 정규표현식

[정규표현식을 체크할 수 있는 사이트](https://regexr.com/)

## 유효성 검사

정규 표현식은 유효성 검사 코드 작성 시 가장 효율적인 방법이다.

```java
import java.util.regex.Pattern;

public class RegexExample {
 public static void main(String[] args)  {
          String name = "홍길동";
          String tel = "010-1234-5678";
          String email = "test@naver.com";
         
          //유효성 검사
          boolean name_check = Pattern.matches("^[가-힣]*$", name);
          boolean tel_check = Pattern.matches("^01(?:0|1|[6-9])-(?:\\d{3}|\\d{4})-\\d{4}$", tel);
          boolean email_check = Pattern.matches("\\w+@\\w+\\.\\w+(\\.\\w+)?", email);

          //출력
          System.out.println("이름 : " + name_check);
          System.out.println("전화번호 : " + tel_check);
          System.out.println("이메일 : " + email_check);
  }
}
```

### **정규식 기본 기호**

| 기호 | 설명 | 예제 |
| --- | --- | --- |
| . | 임의의 문자 1개를 의미 | --- |
| ^ | 시작을 의미한다 [] 괄호 안에 있다면 일치하지 않는 부정의 의미로로 쓰인다 | ^a : a로 시작하는 단어 [^a] : a가 아닌 철자인 문자 1개 |
| $ | $앞의 문자열로 문자가 끝나는지를 의미한다 | a$ : a로 끝나는 단어 |
| [] | [] 괄호 안의 문자가 있는지를 확인한다 | [ab][cd] : a,b중 한 문자와 c,d중 한 문자 → ac ad bc bd |
| [^] | [] 대괄호 안에 ^ 문자가 있으면, 제외를 뜻함 - 대괄호 안에 ^ 가 쓰이면 제외의 뜻 - 대괄호 밖에 ^ 가 쓰이면 시작점의 뜻 | [^a-z] : 알파벳 소문자 a부터 z까지를 제외한 모든 문자 |
| - | 사이의 문자 혹은 숫자를 의미한다 | [a-z] : 알파벳 소문자 a부터 z까지 하나 [a-z0-9] : 알파벳 소문자 전체,0~9 중 한 문자 |
| | | 또는 | [a|b] : a 혹은 b |
| () | 그룹 | 01(0|1) : 01뒤에 0 또는 1이 들어간다 → 010(o), 011(o), 012(x) |
| {} | 개수 | a{3}b : a가 3번 온 후 b가 온다 → aab(x), aaab(o), aaaab(o) |
| \b | 공백, 탭, ",", "/" 등을 의미한다 | apple\b : apple뒤에 공백 탭등이 있다 → apple juice (o), apple.com (x) |
| \B | \b의 부정, 공백 탭등이 아닌 문자인 경우 매치한다 | apple\B → apple.com (o) |
| \d | 0~9 사이의 숫자 [0-9]와 동일 | [a-z] : 알파벳 소문자 a부터 z까지 하나 [a-z0-9] : 알파벳 소문자 전체,0~9 중 한 문자 |
| \D | \d의 부정 숫자가 아닌 어떤 문자, [^0-9]와 동일 |  |
| \s | 공백, 탭 |  |
| \S | 공백, 탭이 아닌 문자 |  |
| \w | 알파벳 대소문자+숫자+"_" [a-zA-Z_0-9]와 동일 |  |
| \W | \w의 부정 [^a-zA-Z_0-9] |  |

### **정규식 수량 기호**

| 기호 | 설명 | 예제 |
| --- | --- | --- |
| ? | 앞의 표현식이 없거나 or 최대 한개만 | a1? : 1이 최대 한개만 있거나 없을수도 있다 → a(o), a1(o), a11(x), a111(x) |
| * | 앞의 표현식이 없거나 or 있거나 (여러개) | a1* : 1이 있을수도 없을수도 있다 → a(o), a1(o), a11(o), a111(o) |
| + | 앞의 표현식이 1개 이상 or 여러개 | a1+ : 1이 1개 이상있다 → a(x), a1(o), a11(o), a111(o) |
| {n} | {n} 딱 n개 있다 | a{3} : a가 딱 3개 있다 → aa(x), aaa(o), aaaa(x), aaaaaaa(x) |
| {n, m} | n개 이상 m개 이하 | a{3,5} : a가 3개 이상 5개 이하 있다 → aa(x), aaa(o), aaaa(o), aaaaaaa(x) |
| {n,}  | n개 이상 a{3,} | a가 3개 이상 있다 → aa(x), aaa(o), aaaa(o), aaaaaaa(o) |

### **정규식 그룹 캡쳐 기호**

| 기호 | 설명 |
| --- | --- |
| () | 그룹 및 캡쳐 |
| (?:) | 찾지만 그룹에 포함 안됨 |
| (?=) | =앞 문자를 기준으로 전방 탐색 |
| (?<=) | =뒤 문자를 기준으로 후방 탐색 |

### **자주 사용되는 정규식 샘플**

| 정규 표현식 | 설명 |
| --- | --- |
| ^[0-9]*$ | 숫자 |
| ^[a-zA-Z]*$ | 영문자 |
| ^[가-힣]*$ | 한글 |
| \\w+@\\w+\\.\\w+(\\.\\w+)? | E-Mail |
| ^\d{2,3}-\d{3,4}-\d{4}$ | 전화번호 |
| ^01(?:0|1|[6-9])-(?:\d{3}|\d{4})-\d{4}$ | 휴대전화번호 |
| \d{6} \- [1-4]\d{6} | 주민등록번호 |
| ^\d{2,3}-\d{3,4}-\d{4}$ | 우편번호 |

### **자바 정규식 문법**

String 클래스의 정규식 문법
String 문자열에 바로 정규표현식을 적용하여 필터링이 가능하다.

String 클래스에서 지원하는 정규식 메소드로는 다음 3가지가 존재한다.

| String 정규 메서드 | 설명 |
| --- | --- |
| boolean matches(String regex) |  인자로 주어진 정규식에 매칭되는 값이 있는지 확인 |
| String replaceAll(String regex, String replacement) | 문자열내에 있는 정규식 regex와 매치되는 모든 문자열을 replacement 문자열로 바꾼 문자열을 반환 |
| String[] split(String regex) | 인자로 주어진 정규식과 매치되는 문자열을 구분자로 분할 |

## Validation을 임포트하면 이하 형식의 데이터를 찾는 정규표현식을 사용할 수 있다

import jakarta.validation.constraints.Pattern;

### **email 주소 유효성 검사 정규표현식**

**'계정@도메인.최상위도메인'** 형식의 데이터를 찾는 정규표현식
![이메일](/assets/email.PNG)

```java
@Pattern(regexp = '^[a-zA-Z0-9+-\\_.]+@[a-zA-Z0-9-]+\\.[a-zA-Z0-9-.]+$')
```

- ^ : 패턴의 시작을 의미
- $ : 패턴의 종료를 의미
- a-zA-Z0-9 (a~z, A~Z, 0~9) : 알파벳(대소문자)+숫자를 의미

### **휴대폰 번호 유효성 검사 정규표현식**

**'3자리 숫자 - 3자리 or 4자리 숫자 - 4자리 숫자'** 형식의 데이터를 찾는 정규표현식

```java
@Pattern(regexp = '\d{3}-\d{3,4}-\d{4}')
```

### **비밀번호 유효성 검사 정규표현식**

**'최소 8 자, 최소 하나의 문자, 하나의 숫자 및 하나의 특수 문자'** 형식의 데이터를 찾는 정규표현식

```java
@Pattern(regexp = '^(?=.*[A-Za-z])(?=.*\d)[?=.*[@!%*#?&]](A-Za-z\d@!%*#?&){8,}$')
```
