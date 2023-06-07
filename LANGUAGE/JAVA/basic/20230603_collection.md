# **Collection** (참조형 분류통)

Java 프로그래밍 에서는 배열을 더 고도화 시켜서 `컬렉션` 이라는 이름으로 🗳️참조형 분류통(자료구조)를 제공하고 있다. 컬렉션은 참조형 변수만 저장함으로써 여러 기능을 많이 제공한다.

컬렉션은 여러가지 종류가 있고, 이러한 컬렉션들은 데이터를 넣고 빼는 방법이 각자 다르기 때문에 용도에 맞게 사용합니다.

## 1. 컬렉션🧬 이해

- Java 에서 컬렉션🧬 은 배열보다 다수의 참조형 데이터를 더 쉽고 효과적으로 처리할 수 있는 기능을 많이 가지고 있다.
  - 컬렉션🧬 기능 : 크기 자동조정/ 추가/ 수정/ 삭제/ 반복/ 순회/ 필터/ 포함확인 등….
- 컬렉션🧬 종류
  - `Collection` 에는 `List`, `Set` , `Queue` , `Map` 이 있습니다.
    - `List` : 순서가 있는 데이터의 집합 (데이터 중복 허용) - 배열과 비슷
    - `Queue` : 빨대🥤처럼 한쪽에서 데이터를 넣고 반대쪽에서 데이터를 뺄 수 있는 집합
    (`First In First Out` : 먼저들어간 순서대로 값을 조회할 수 있다.)
    - `Set` : 순서가 없는 데이터의 집합 (데이터 중복 허용 안함) - 순서없고 중복없는 배열
    - `Map` : 순서가 없는 (`Key,Value`) 쌍으로 이루어진 데이터의 집합 (Key값 중복 허용 안함)

- Collection🧬 은 기본형 변수가 아닌 참조형 변수를 저장한다!

❓ 자주쓰는 **참조형 변수**

- `int` 의 참조형 변수 = `Integer`
- `long` 의 참조형 변수 = `Long`
- `double` 의 참조형 변수 = `Double`
- `String` 은 원래부터 참조형 변수

## 1. Array 와 ArrayList

📌 ArrayList 는 배열(Array)처럼 일렬로 데이터를 저장하고 조회하여 순번값(인덱스)로 값을 하나씩 조회할 수 있다. 배열(Array)처럼 크기가 정해져 있지않고 필요할때마다 크기가 점점 더 늘어난다.

- **`Array`** 은 메모리에 연속된 공간을 `요청한 사이즈 만큼` 받아서 `실제값을 저장`하는 기본형 변수로 저장한다. 이렇게 크기를 고정하여 생성하는 것을 **`정적배열`** 이라고 한다.

- **`ArrayList`** 는 생성시점에 작은 연속된 공간을 요청 해서 참조형 변수들을 담아놓고, `값이 추가될때` 더 큰 공간이 필요하면 `더큰 공간을 받아서 저장`한다. 이렇게 크기가 가변적으로 늘어나는 것을 **`동적배열`** 이라고 한다.

1) 선언 : `ArrayList<Integer> intList` 형태로 선언한다.
2) 생성 : `new ArrayList<Integer>();` 형태로 생성한다.
3) 초기화 : 사이즈를 지정하는것이 없기 때문에 초기화가 필요 없다.
4) 값 추가 : `intList.add({추가할 값})` 형태로 값을 추가한다.
5) 값 수정 : `intList.set({수정할 순번}, {수정할 값})` 형태로 값을 수정한다.
6) 값 삭제 : `intList.remove({삭제할 순번})` 형태로 값을 삭제한다.
7) 전체 출력 : `intList.toString()` 형태로 전체 값을 대괄호`[]`로 묶어서 출력한다.
8) 전체 제거 : `intList.clear()` 형태로 전체 값을 삭제한다.

```java
// ArrayList 
// (사용하기 위해선 import java.util.ArrayList; 를 추가해야합니다.)
import java.util.ArrayList;

public class Main {

    public static void main(String[] args) {
        ArrayList<Integer> intList = new ArrayList<Integer>(); // 선언 및 생성
        
        intList.add(1);
        intList.add(2);
        intList.add(3);
        
        System.out.println(intList.get(0)); // 1 출력
        System.out.println(intList.get(1)); // 2 출력
        System.out.println(intList.get(2)); // 3 출력
        System.out.println(intList.toString()); // [1,2,3] 출력
        
        intList.set(1, 10); // 1번순번의 값을 10으로 수정합니다.
        System.out.println(intList.get(1)); // 10 출력
        
        
        intList.remove(1); // 1번순번의 값을 삭제합니다.
        System.out.println(intList.toString()); // [1,3] 출력
        
        intList.clear(); // 전체 값을 삭제합니다.
        System.out.println(intList.toString()); // [] 출력
    }
}
```

## 2. LinkedList

📌 `LinkedList` 는 메모리에 남는 공간을 요청해서 여기저기 나누어서 실제값을 담아놓고, 실제값이 있는 주소값으로 목록을 구성하고 저장한다.

- 기본적인 기능은 `ArrayList` 와 동일하지만 `LinkedList` 는 값을 나누어 담기 때문에 모든값을 조회하는 속도가 느리다. 대신에, 값을 중간에 추가하거나 삭제할때는 속도가 빠르다.
- 중간에 값을 추가하는 기능이 있다. (속도 빠름)

1) 선언 : `LinkedList<Integer> linkedList` 형태로 선언
2) 생성 : `new LinkedList<Integer>();` 형태로 생성
3) 초기화 : 사이즈를 지정하는것이 없기 때문에 초기화가 필요 없음
4) 값 추가 : `linkedList.add({추가할 값})` 형태로 값을 추가
5) 값 중간에 추가 : `linkedList.add({추가할 순번}, {추가할 값})` 형태로 값을 중간에 추가
6) 값 수정 : `linkedList.set({수정할 순번}, {수정할 값})` 형태로 값을 수정
7) 값 삭제 : `linkedList.remove({삭제할 순번})` 형태로 값을 삭제
8) 전체 출력 : `linkedList.toString()` 형태로 전체 값을 대괄호`[]`로 묶어서 출력
9) 전체 제거 : `linkedList.clear()` 형태로 전체 값을 삭제

```java
// LinkedList 
// (사용하기 위해선 import java.util.LinkedList; 를 추가해야합니다.)
import java.util.LinkedList;

public class Main {

    public static void main(String[] args) {
        LinkedList<Integer> linkedList = new LinkedList<>(); // 선언 및 생성

        linkedList.add(1);
        linkedList.add(2);
        linkedList.add(3);

        System.out.println(linkedList.get(0)); // 1 출력
        System.out.println(linkedList.get(1)); // 2 출력
        System.out.println(linkedList.get(2)); // 3 출력
        System.out.println(linkedList.toString()); // [1,2,3] 출력 (속도 느림)

        linkedList.add(2, 4); // 2번 순번에 4 값을 추가합니다.
        System.out.println(linkedList); // [1,2,4,3] 출력

        linkedList.set(1, 10); // 1번순번의 값을 10으로 수정합니다.
        System.out.println(linkedList.get(1)); // 10 출력

        linkedList.remove(1); // 1번순번의 값을 삭제합니다.
        System.out.println(linkedList); // [1,4,3] 출력

        linkedList.clear(); // 전체 값을 삭제합니다.
        System.out.println(linkedList); // [] 출력
    }
}
```

## 3. Stack (LIFO)

📌 `Stack` 은 값을 수직으로 쌓아놓고 넣었다가 빼서 조회하는 형식으로 데이터를 관리 합니다.

이걸 **“나중에 들어간 것이 가장 먼저 나온다(`Last-In-First-out`)”** 성질을 가졌다고 표현하며, 주로 상자 또는 일방통행 길 생각하면 됨

- 상자에 물건을 넣고 빼는것처럼 밑에서 위로 쌓고, 꺼낼때는 위에서 부터 꺼내는 형식
- 그렇기 때문에 넣는 기능(`push()`) 과 조회(`peek()`), 꺼내는(`pop()`) 기능만 존재
- 이렇게 불편하게 쓰는 이유는 최근 저장된 데이터를 `나열`하고 싶거나 데이터의 `중복처리`를 막고싶을때 사용

1) 선언 : `Stack<Integer> intStack` 형태로 선언
2) 생성 : `new Stack<Integer>();` 형태로 생성
3) 추가 : `intStack.push({추가할 값})` 형태로 값을 추가
4) 조회 : `intStack.peek()` 형태로 맨 위값을 조회
5) 꺼내기 : `intStack.pop()` 형태로 맨 위값을 꺼냄 (꺼낸 후엔 삭제됨)

```java
// Stack 
// (사용하기 위해선 import java.util.Stack; 를 추가해야합니다.)
import java.util.Stack;

public class Main {

    public static void main(String[] args) {
        Stack<Integer> intStack = new Stack<Integer>(); // 선언 및 생성
        
        intStack.push(1);
        intStack.push(2);
        intStack.push(3);

        while (!intStack.isEmpty()) { // 다 지워질때까지 출력
            System.out.println(intStack.pop()); // 3,2,1 출력
        }

        // 다시 추가
        intStack.push(1);
        intStack.push(2);
        intStack.push(3);
        
        // peek()
        System.out.println(intStack.peek()); // 3 출력
        System.out.println(intStack.size()); // 3 출력 (peek() 할때 삭제 안됬음)
        
        // pop()
        System.out.println(intStack.pop()); // 3 출력
        System.out.println(intStack.size()); // 2 출력 (pop() 할때 삭제 됬음)
        
        System.out.println(intStack.pop()); // 2 출력
        System.out.println(intStack.size()); // 1 출력 (pop() 할때 삭제 됬음)

        while (!intStack.isEmpty()) { // 다 지워질때까지 출력
            System.out.println(intStack.pop()); // 1 출력 (마지막 남은거 하나)
        }
    }
}
```

## 4. Queue 🥤 (FIFO)

📌 `Queue` 는 빨대🥤처럼 한쪽에서 데이터를 넣고 반대쪽에서 데이터를 뺄 수 있는 집합

- First In First Out : 먼저들어간 순서대로 값을 조회
- 그렇기 때문에 넣는 기능(`add()`),  조회(`peek()`), 꺼내는(`poll()`) 기능만 존재
- `Queue` 는 생성자가 없는 껍데기라서 바로 생성할수는 없다. (껍데기 = 인터페이스)
- 생성자가 존재하는 클래스인 `LinkedList` 를 사용하여 `Queue` 를 생성해서 받을 수 있음

```java
// LinkedList 를 생성하면 Queue 기능을 할 수 있습니다. (Queue 가 부모/ LinkedList 가 자식이기 떄문)
Queue<Integer> intQueue = new LinkedList<Integer>();
```

1) 선언 : `Queue<Integer> intQueue` 형태로 선언
2) 생성 : `new LinkedList<Integer>();` 형태로 생성
3) 추가 : `intQueue.add({추가할 값})` 형태로 값을 맨 위에 추가
4) 조회 : `intQueue.peek()` 형태로 맨 아래값을 조회
5) 꺼내기 : `intQueue.poll()` 형태로 맨 아래값을 꺼냄 (꺼내고나면 삭제됨)

```java
// Queue 
// (사용하기 위해선 java.util.LinkedList; 와 import java.util.Queue; 를 추가해야합니다.)
import java.util.LinkedList;
import java.util.Queue;

public class Main {

public static void main(String[] args) {
    Queue<Integer> intQueue = new LinkedList<>(); // 선언 및 생성

    intQueue.add(1);
    intQueue.add(2);
    intQueue.add(3);

    while (!intQueue.isEmpty()) { // 다 지워질때까지 출력
        System.out.println(intQueue.poll()); // 1,2,3 출력
    }

    // 다시 추가
    intQueue.add(1);
    intQueue.add(2);
    intQueue.add(3);

    // peek()
    System.out.println(intQueue.peek()); // 1 출력 (맨먼저 들어간값이 1 이라서)
    System.out.println(intQueue.size()); // 3 출력 (peek() 할때 삭제 안됬음)

    // poll()
    System.out.println(intQueue.poll()); // 1 출력
    System.out.println(intQueue.size()); // 2 출력 (poll() 할때 삭제 됬음)

    System.out.println(intQueue.poll()); // 2 출력
    System.out.println(intQueue.size()); // 1 출력 (poll() 할때 삭제 됬음)

    while (!intQueue.isEmpty()) { // 다 지워질때까지 출력
        System.out.println(intQueue.poll()); // 3 출력 (마지막 남은거 하나)
    }
}
}
```

## 4. Set 📚

📌 `Set` 은 순서가 없는 데이터의 집합 (데이터 중복 허용 안함) - 순서없고 중복없는 배열

- 순서가 보장되지 않는 대신 중복을 허용하지 않도록 유지할 수 있음
- `Set` 은 그냥 `Set`으로 쓸수도있지만 `HashSet`, `TreeSet` 등으로 응용하여 사용할 수 있음
- `Set` 는 생성자가 없는 껍데기라서 바로 생성할수는 없음 (껍데기 = 인터페이스)
- 생성자가 존재하는 클래스인 `HashSet` 를 사용하여 `Set` 를 생성해서 받을 수 있음

1) 선언 : `Set<Integer> intSet` 형태로 선언
2) 생성 : `new HashSet<Integer>();` 형태로 생성
3) 추가 : `intSet.add({추가할 값})` 형태로 값을 맨 위에 추가
4) 조회 : `intSet.get({초회할 순번})` 형태로 순번에 있는 값을 조회
5) 삭제 : `intSet.remove({삭제할 값})` 형태로 삭제할 값을 직접 지정
6) 포함확인 : `intSet.contains({포함확인 할 값})` 형태로 해당값이 포함되어있는지 boolean 값으로 응답

🔎 `HashSet` 외에도 `TreeSet`, `LinkedHashSet` 이 있다.

- `HashSet` : 가장 빠르기때문에 일반적으로 사용하지만 순서를 전혀 예측할 수 없음
- `TreeSet` : 정렬된 순서대로 보관하며 정렬 방법을 지정할 수 있음
- `LinkedHashSet` : 추가된 순서, 또는 가장 최근에 접근한 순서대로 접근 가능하기때문에 순서보장이 필요한 경우에 주로 사용함

```java
// Set 
// (사용하기 위해선 import java.util.Set; 와 java.util.HashSet; 를 추가해야합니다.)
import java.util.HashSet;
import java.util.Set;

public class Main {

public static void main(String[] args) {
    Set<Integer> intSet = new HashSet<Integer>(); // 선언 및 생성

    intSet.add(1);
    intSet.add(2);
    intSet.add(3);
    intSet.add(3); // 중복된 값은 덮어씁니다.
    intSet.add(3); // 중복된 값은 덮어씁니다.

    for (Integer value : intSet) {
        System.out.println(value); // 1,2,3 출력
    }

    // contains()
    System.out.println(intSet.contains(2)); // true 출력
    System.out.println(intSet.contains(4)); // false 출력

    // remove()
    intSet.remove(3); // 3 삭제

    for (Integer value : intSet) {
        System.out.println(value); // 1,2 출력
    }
}
}
```

## 5. Map 👫

📌 Map 은 key-value 구조로 구성된 데이터를 저장한다

- key-value 형태로 데이터를 저장하기 때문에 기존에 순번으로만 조회하던 방식에서, key 값을 기준으로 vlaue를 조회
- key 값 단위로 중복을 허용하지 않는 기능
- `Map` 은 그냥 `Map`으로 쓸수도있지만 `HashMap`, `TreeMap`등으로 응용하여 사용가능
- `Map`으로 쓸수도있지만 `HashSet`, `TreeSet` 등으로 응용하여 사용가능

1) 선언 : `Map<String, Integer> intMap` 형태로 Key타입과 Value타입을 지정해서 선언
2) 생성 : `new` `HashMap<>();` 형태로 생성
3) 추가 : `intMap.put({추가할 Key값},{추가할 Value값})` 형태로 Key에 Value값을 추가
4) 조회 : `intMap.get({조회할 Key값})` 형태로 Key에 있는 Value값을 조회
5) 전체 key 조회 : `intMap.keySet()` 형태로 전체 key 값들을 조회
6) 전체 value 조회 : `intMap.values()` 형태로 전체 value 값들을 조회
7) 삭제 : `intMap.remove({삭제할 Key값})` 형태로 Key에 있는 Value값을 삭제

🔎 `HashMap` 과 `TreeMap`

- `HashMap` : 중복을 허용하지 않고 순서를 보장하지 않음 , 키와 값으로 `null이 허용`
- `TreeMap` : key 값을 기준으로 정렬을 할 수 있습니다. 다만, 저장시 `정렬(오름차순)`을 하기 때문에 저장시간이 다소 오래 걸림

```java
// Map 
// (사용하기 위해선 import java.util.Map; 를 추가해야합니다.)
import java.util.Map;

public class Main {

    public static void main(String[] args) {
        Map<String, Integer> intMap = new HashMap<>(); // 선언 및 생성

        //          키 , 값
        intMap.put("일", 11);
        intMap.put("이", 12);
        intMap.put("삼", 13);
        intMap.put("삼", 14); // 중복 Key값은 덮어씁니다.
        intMap.put("삼", 15); // 중복 Key값은 덮어씁니다.

        // key 값 전체 출력
        for (String key : intMap.keySet()) {
            System.out.println(key); // 일,이,삼 출력
        }

        // value 값 전체 출력
        for (Integer key : intMap.values()) {
            System.out.println(key); // 11,12,15 출력
        }

        // get()
        System.out.println(intMap.get("삼")); // 15 출력
    }
}
```

## 🔎 **length vs length() vs size()** - 길이값 가져오기

### 1. length

- arrays(int[], double[], String[])
- `length`는 배열의 길이를 조회

### 2. length()

- String related Object(String, StringBuilder etc)
- `length()`는 문자열의 길이를 조회 (eg. “ABCD”.length() == 4)

### 3. size()

- Collection Object(ArrayList, Set etc)
- `size()`는 컬렉션 타입목록의 길이를 조회
