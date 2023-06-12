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

정규 표현식에 대상 문자열을 검증하는 기능은 java.util.rege.Pattern 클래스의 matches()메소드를 활용하여 검증할 수 있다. matches() 메서드의 첫번째 매개값은 정규표현식이고 두번째 매개값은 검증 대상 문자열이다. 검증 후 대상문자열이 정규표현식과 일치하면 true, 그렇지 않다면 false값을 리턴한다.

날짜와 전화번호를 입력받을때 이를 사용하였다.

## 자주 사용하는 정규표현식

[정규표현식을 체크할 수 있는 사이트](https://regexr.com/)

 ![정규표현식](/assets/regex.PNG)

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
