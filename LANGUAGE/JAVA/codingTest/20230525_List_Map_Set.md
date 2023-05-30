# HW . List Map Set

## **자료구조 요리 레시피 메모장 만들기**

- 입력값
  - 저장할 자료구조명을 입력합니다. (List / Set / Map)
  - 내가 좋아하는 요리 제목을 먼저 입력합니다.
  - 이어서 내가 좋아하는 요리 레시피를 한문장씩 입력합니다.
  - 입력을 마쳤으면 마지막에 “끝” 문자를 입력합니다.
- 출력값
  - 입력이 종료되면 저장한 자료구조 이름과 요리 제목을 괄호로 감싸서 먼저 출력 해줍니다.
  - 이어서, 입력한 모든 문장앞에 번호를 붙여서 입력 순서에 맞게 모두 출력 해줍니다.

### 입력예시

```java
Set
백종원 돼지고기 김치찌개 만들기
돼지고기는 핏물을 빼주세요.
잘익은 김치 한포기를 꺼내서 잘라주세요.
냄비에 들기름 적당히 두르고 김치를 넣고 볶아주세요.
다진마늘 한스푼, 설탕 한스푼 넣어주세요.
종이컵으로 물 8컵 부어서 센불에 끓여주세요.
핏물 뺀 돼지고기를 넣어주세요.
된장 반스푼, 양파 반개, 청양고추 한개를 썰어서 넣어주세요.
간장 두스푼반, 새우젓 두스푼, 고춧가루 두스푼반 넣어주세요.
중불로 줄여서 오래 끓여주세요~!
마지막에 파 쏭쏭 썰어서 마무리하면 돼요^^
끝
```

### 출력예시

```java
  [ 백종원 돼지고기 김치찌개 만들기 ]
  별점 : 4 (80.0%)
  1. 돼지고기는 핏물을 빼주세요.
  2. 잘익은 김치 한포기를 꺼내서 잘라주세요.
  3. 냄비에 들기름 적당히 두르고 김치를 넣고 볶아주세요.
  4. 다진마늘 한스푼, 설탕 한스푼 넣어주세요.
  5. 종이컵으로 물 8컵 부어서 센불에 끓여주세요.
  6. 핏물 뺀 돼지고기를 넣어주세요.
  7. 된장 반스푼, 양파 반개, 청양고추 한개를 썰어서 넣어주세요.
  8. 간장 두스푼반, 새우젓 두스푼, 고춧가루 두스푼반 넣어주세요.
  9. 중불로 줄여서 오래 끓여주세요~!!
  10. 마지막에 파 쏭쏭 썰어서 마무리하면 돼요^^
```

### 1) 🔑 힌트

- 계속 반복하면서 입력받기

```java
ArrayList<String> strList = new ArrayList<>();
while(true) {
  String text = sc.next();
  strList.add(text);
}
```

- if 문으로 끝 확인하고 반복문 종료하기

```java
while(true) {
  String text = sc.next();
  if (text == "끝") {
    break;
  }
}
```

- LinkedHashSet 선언 후 순회하기

```java
LinkedHashSet<String> strSet = new LinkedHashSet<>(); // 선언
// ... 중략 ...
Iterator iterator = strSet.iterator();
// strList 한줄씩 출력
for (int i = 0; i < strSet.size(); i++) {
  int number = i + 1;
  System.out.println(number + ". " + iterator.next());
}
```

- HashMap 선언 후 한줄씩 입력받기

```java
Map<Integer, String> strMap = new HashMap<>();
int lineNumber = 1;
while (true) {
	// 한줄씩 입력받아서 strList 에 저장
	String text = sc.next();
	if (Objects.equals(text, "끝")) {
		break;
	}
	strMap.put(lineNumber++, text);
}
```

![2주차 숙제](/assets/2%EC%A3%BC%EC%B0%A8%EB%A6%AC%EC%8A%A4%ED%8A%B8.PNG)
![2주차 숙제](/assets/2%EC%A3%BC%EC%B0%A8%EC%85%8B.PNG)
![2주차 숙제](/assets/2%EC%A3%BC%EC%B0%A8%EB%A7%B5.PNG)

오류는 없었지만 혼자 하라고하면 못할것 같다.
연습 많이해야지
