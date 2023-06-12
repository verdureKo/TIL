# 호텔 예약 프로그램_01

2시간 가까이 회의를 하고 요구사항을 반영하여 작업을 했고 모든팀원들이 사실 5일에 작업을 마쳤었다.
오늘 버그픽스만 하고 끝났다고 생각이 드는데 조바심이 늘어만 간다😨 어떻게 그렇게 다들 한번에 보고 하는거지
심지어 오늘 내가 실수를 했는데도 모두 차분했다. 뭔가 우리집만 불난 호떡집같다.
마음도 급하고 코드도 급하고..

## 호텔 예약 확인 부분

```java
public void reservationComplete(Room room, Customer customer, String date) {
        System.out.println();
        System.out.println("------ 예약 완료 페이지 ------");
        Reservation reservation = null;
        if (customer != null) {
            reservation = new Reservation(room, customer.getName(), customer.getPhone(), date);
            reservationList.add(reservation);
            room.setDateList(date);
            System.out.println("예약이 완료되었습니다.");
            System.out.println("고객님의 예약 번호는 " + reservation.getId() + "입니다.");
        } else {
            System.out.println("예약이 불가합니다. 메인 화면으로 돌아갑니다.");
        }
    } // reservationComplete()
```

아직도 어떻게 필드를 불러서 쓰는건지 잘 모르겠다..
같은 팀원분이 모자란 날 배려해(?) 주석까지 친절하게 달아주셨는데 그걸 또 못알아듣고 제대로 필드를 못불러와서 뻘겋게 물들이는건지 너무 속상하다. 묘하게 맞고 묘하게 다틀려놔서 이번에도 역시 크게 도움을 받았다 😫
이미 선언이 되어있는건 저렇게 불러다 쓸수있는거였다. 연휴내내 헛짓만 무한반복했는데 책을봐도 응용은 못하겠고 이거원.. 튜터님이 앞으로도 도움요청을 많이하고 다른동료도 도와줄 수 있는사람으로 성장하라고 말씀해주셔서 조금은 위안이 되었지만 자괴감을 이겨내는게 쉽지가 않다.

## 호텔 예약 조회 부분 (a.k.a 내가 빻아버린 부분🙉)

```java
public void showAllReservation() {
        System.out.println();
        System.out.println("------ 예약 내역 관리자 페이지 ------");
        System.out.println("관리자 비밀번호를 입력해주세요: ");
        Scanner sc = new Scanner(System.in);
        while (true) {
            String inputPassword = sc.nextLine();

            if (inputPassword.equals(password)) {
                if (reservationList.isEmpty()) {
                    System.out.println("예약 내역이 존재하지 않습니다.");
                } else {
                    for (Reservation r : reservationList) {
                        System.out.printf("%s | %-4.1f | %-5s | %12s | %10s | %s\n", r.getRoom().getRoomSize(), r.getRoom().getRoomCharge(), r.getCustomerName(), r.getPhoneNumber(), r.getReservationDate(), r.getId());
                    }
                }
                break;
            } else {
                System.out.println("다시 입력해주세요.");
            }
        } // while()
        System.out.println("\n3초 후 메인 메뉴로 돌아갑니다.");
        try {
            Thread.sleep(3000);
        } catch (InterruptedException e) {
            System.out.println(e.getMessage());
        }
    } // showAllReservation()

```

if (reservationList.isEmpty()) {} 요 if문 위치를 잘못써서 물레방아를 연성해놓고 신나서 커밋푸쉬를 해놓고 루룰루 과자하나 먹고오니 모두 에러가 난다고 채팅창이 닥근해져있었다..모두 괜찮다 해주었지만 정말 쓸데없는짓으로 에러가 없던 코드에 에러를 추가한게 후회가 몰려왔지만 앞으로 테스트는 꼭 중지하고 재실행 해야겠다, 돌던것들 다 끄고 실행해야겠다는 교훈을 얻었다 ㅠㅠ..
분명히 에러가 안나서 했었는데 왜때문에 안났을까 하고 팀원들에게 물어보니 중지를 제대로 안하고 재실행만 계속하면 그렇게 되는경우가 있다고한다.

## 개인과제 피드백

- 전체적으로 기능도 잘 짜셨고 기능도 대부분 잘 동작하는것으로 보입니다. 처음에 막막하셨을텐데 도움받으면서 완성하느라 고생 많으셨습니다. 혼자 성장하는 개발자는 없으니 앞으로도 도움요청도 많이하고 다른 동료들도 도와줄 수 있는 개발자로 성장해주세요.
- 메서드명은 생성자 메서드가 아니라면 소문자로 시작해야 합니다. (예를들어 Menu() 가 아니라 menu() 가 돼야겠죠.)
- Menu 클래스와 Items 클래스의 순번(index) 필드가 문자열로 되어있던데 숫자로 하는것이 연산속도도 좋고 에러방지에도 좋습니다.
- Items 클래스가 있던데 클래스명은 복수가 아닌 단수로 표현해주세요. 그렇다면 Item 이 돼야겠죠?
- Items 클래스에서 Menu 클래스를 상속받으면서 getIndex, getName 같은 메서드를 Override 하셨던데 추가적인 구현내용이 없기때문에 따로 메서드를 선언해주지 않아도 Menu 의 getIndex, getName 메서드를 그대로 사용할 수 있습니다. Items 에 새로 추가된 필드인 price 값에 대한 getPrice 메서드만 추가해주시면 됬었을것 같아요.
- 주석을 틈틈히 달아주신것 훌륭합니다. 다만, 동작에 대한 주석이 좀더 추가되면 좋겠고 깃 커밋도 많이 세분화해서 어떤 기능에 대한 수정사항인지 표시해주는게 좋아요.

[피드백 적용링크](https://github.com/verdureKo/Kiosk/tree/main/src)

오늘하루도 팀원님들에게 너무나 감사한 하루다.
