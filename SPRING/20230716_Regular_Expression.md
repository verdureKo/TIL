
# Regular Expression

1. 정규 표현식(Regular Expression)

   문자열이 정해져 있는 형식으로 구성되어 있는지 검증할 때 사용합니다.

   [예시 : 이메일, 전화번호, 비밀번호 등]

2. java.util.regex 패키지 Class Pattern : JAVA 공식 Document 참고

   https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html#sum

3. java.util.regex 패키지 Class Matcher : JAVA 공식 Document 참고

   https://docs.oracle.com/javase/8/docs/api/java/util/regex/Matcher.html#sum

4. 정규식 예시

   ※ Java - 정규표현식(regex), 다양한 예제로 쉽게 이해하기
      https://codechacha.com/ko/java-regex/ 

   ※ 정규표현식 변환 웹사이트 참고 활용 = http://regexr.com

      ① 좌측 Cheatsheet 클릭 - Character classes 클릭 - 그러면 character set, negated set, range, dot, match any,
                                                                               word, not word, digit, not digit, whitespace 가 나타남

      ② 좌측 Character classes 리스트 항목들을 클릭해 보면서, Example에 나타나는 정규 표현식을 참고 바랍니다.

      ③ 중앙 Expression 에서 /.../g 안에 ... 부분에 ([A-Z])\w+ 정규식을 넣고, 즉, /([A-Z])\w+/g 정규표현식에서
 
          하단의 "Text" 음영 표시 변화와 하단의 "Explain"을 설명을 참고하시기 바랍니다.

          Expression 에서 /.../g 안에 내용을 https://codechacha.com/ko/java-regex/ 웹사이트 참고해서

          다양하게 정규 표현식을 넣어보고, 하단의 "Text" 음영 표시 변화와 하단의 "Explain"을 설명을 참고하시기 바랍니다.

  1) 전화번호 : http://regexr.com

     (02|010)-\d{3,4}-\d{4} // 02또는010-3자리부터4자리까지-정확히4자리입력되어야 함

  2) 정규식 변환 웹사이트 : http://regexr.com

    ① 좌측 상단 New 버튼 클릭

    ② 좌측 Cheatsheet 클릭 - Character classes 클릭 - 그러면 character set, negated set, range, dot, match any,
                                                                             word, not word, digit, not digit, whitespace 가 나타남

    ③ 우측 Expression /./g 에서 . 자리에 (02|010) 입력(/(02|010)/g) 하고, Text  입력창에 02, 010, 2, 01 숫자들을 입력하면 02, 010만 음영 표시됨.
        즉, 패턴 검증됨을 나타냄. 우측 하단에 Explain 클릭 확인 바람.
        이런 방법으로 (02|010)-\d{3,4}-\d{4} 패턴 입력 후 010-1234-1111 패턴도 체크해 보기 바람. 참고로, \w는 word 인식을 말함.
        그리고,  \w+@\w+\.\w+(\.\w+)? 패턴 입력 후 test@google.com 패턴도 체크해 보기 바람.

    * 정규식 예시 : 참고 웹사이트 https://www.youtube.com/watch?v=1BTGSVhNDu8

  2) 이메일 : test@google.com, test@goole.co.kr
      \w+@\w+\.\w+(\.\w+)? // 한개이상의알파벳(또는숫자)@한개이상의알파벳(또는숫자).한개이상의알파벳(또는숫자).한개이상의알파벳(또는숫자)없음또는한개이상

  3) Pattern 클래스 : 정규 표현식으로 문자열을 검증하는 역할
      boolean result = Pattern.matches("정규식", "입력된 문자열");

  [WebSocketEx 프로젝트 BroadSocket.java]

  // 메시지에서 유저 명을 취득하기 위한 정규식 표현 적용 가능함. Pattern.compile(""); // "" 안에 정규식 넣으면 됨
   private static Pattern pattern = Pattern.compile(""); 
  // 자바에서 \를 표현하려면 \\처럼 사용해야 합니다.
  // ^는 문자열의 시작을 나타냅니다. 따라서 ^ 다음으로 오는 패턴으로 문자열이 시작되는 것을 찾습니다.
  // 즉, ^regex 는 ^ 다음 regex로 line을 시작하는지 의미합니다.
  // {X}는	X회 이상 반복함을 의미합니다. 참고로, {X,Y} 는 X~Y 사이의 수만큼 반복함을 의미합니다.
  // . 는 어떤 문자 1개를 의미합니다.
  // *? 는 가장 적게 일치하는 패턴을 찾음
  // 참고로, *은 * 앞의 요소가 0이상 반복되는 것을 의미합니다.
  // 그리고, ?는 요소가 0 또는 1회만 반복되는 것을 의미합니다.
  
  // 변수의 상수화 : replaceAll (패턴에 맞는 값을 새로운 값으로 치환)
  // replaceAll(regex, replacement)은 regex와 일치하는 내용을 replacement로 교체합니다.
    final String msg = message.replaceAll(pattern.pattern(), "");
   // String.replaceFirst(regex, replacement) : regex와 가장 먼저 일치하는 것을 replacement로 변환
   // $ 는 문자열의 종료를 의미합니다. name.replaceFirst("", "").replaceFirst("", ""); // "", "" 각각의 첫번째 "" 안에 정규식 넣으면 됨
    final String username = name.replaceFirst("", "").replaceFirst("", "");

5. Java - 정규표현식(regex), 다양한 예제로 쉽게 이해하기
   https://codechacha.com/ko/java-regex/ 

6. 정규식 변환 웹사이트 : http://regexr.com

   1) 좌측 상단 New 버튼 클릭

   2) 좌측 Cheatsheet 클릭 - Character classes 클릭 - 그러면 character set, negated set, range, dot, match any,
                                                                             word, not word, digit, not digit, whitespace 가 나타남

   3) 중앙 Expression /./g 에서 . 자리에 \\ 입력(/\\/g) 하고, Text  입력창에 \ 문자 입력하면 음영 표시됨.
       즉, 패턴 검증됨을 나타냄. 우측 하단에 Explain 클릭 확인 바람

      그런데, \\ 앞에 ^ 문자를 입력하면, 즉, ^\\ 라고 하면, \ 문자로 시작하는 \만 음영으로 표시됨. 그 이후 \에는 음영 표지 안됨.

   4) /./g 에서 . 자리에 {\\{ 입력(/{\\{/g) 하고,  Text  입력창에 {\{ 문자 입력하면 음영 표시됨.

   5)  /./g 에서 . 자리에 .*?\\ 입력(/.*?\\/g) 하면,  Text  입력창에 \ 문자가 입력되면 음영 표시됨.

   6) /./g 에서 . 자리에 \\} 입력(/\\}/g) 하면,  Text  입력창에 입력되어 있는 \} 문자가 음영 표시됨.

   7) $ 는 문자열의 종료를 의미함.

   8) BroadSocket.java 파일에 다음과 같이 정규식 표현을 적용하고 채팅 실행 확인을 해봅니다.

     // 메시지에서 유저 명을 취득하기 위한 정규식 표현                         // http://regexr.com 웹에서 중앙 Expression /[A-Z]/g 입력하고 Text 입력창 문자 입력 확인해 봄
        private static Pattern pattern = Pattern.compile("^\\{\\{.*?\\}\\}"); // [A-Z] 정규표현식도 적용하고 대화명 Jang, 메시지 AAA, Abc, aaa 채팅 실행 확인하기 바람

    // 변수의 상수화 : replaceAll (패턴에 맞는 값을 새로운 값으로 치환)
    // replaceAll(regex, replacement)은 regex와 일치하는 내용을 replacement로 교체합니다.
       final String msg = message.replaceAll(pattern.pattern(), "");
    // String.replaceFirst(regex, replacement) : regex와 가장 먼저 일치하는 것을 replacement로 변환 
    // $ 는 문자열의 종료를 의미합니다.                                                                      // http://regexr.com 웹에서 중앙 Expression /[A-Z]/g 입력하고 Text 입력창 문자 입력 확인해 봄
       final String username = name.replaceFirst("^\\{\\{", "").replaceFirst("\\}\\}$", ""); // replaceFirst() 메서드 각각에 [A-Z] 정규표현식도 적용하고 대화명 Jang, 메시지 AAA, Abc, aaa 채팅 실행 확인하기 바람

7. 정규표현식 테스트 사이트(regexr.com) : 다음의 웹사이트 하단 "참고자료 주요내용" 보기 바람

   https://pyh13701.tistory.com/31

8. [Java] 자바 정규 표현식 (Pattern, Matcher) 사용법 & 예제

   https://coding-factory.tistory.com/529

9. 자바 정규식 기본정리 : Matcher, Pattern, find(), group()

   https://blog.naver.com/bb_/220863282423

10. Java 정규식 테스트 사이트 : https://www.regexplanet.com/advanced/java/index.html

   https://cofs.tistory.com/359

11. Regular Expression Test Page for Java

   https://www.regexplanet.com/advanced/java/index.html

12. 정규 표현식 패턴들 : https://zvon.org/

    https://www.youtube.com/watch?v=V_ePeBaQzSc&list=PLB9NsRTifc1nc8J5BJhkE3AP9oieECVpJ&index=1
    https://www.youtube.com/watch?v=KT7Pk6oFOx4&list=PLB9NsRTifc1nc8J5BJhkE3AP9oieECVpJ&index=2
    https://www.youtube.com/watch?v=hYrTh5Q8tIM&list=PLB9NsRTifc1nc8J5BJhkE3AP9oieECVpJ&index=3
    https://www.youtube.com/watch?v=hYrTh5Q8tIM&list=PLB9NsRTifc1nc8J5BJhkE3AP9oieECVpJ&index=4
    https://www.youtube.com/watch?v=hYrTh5Q8tIM&list=PLB9NsRTifc1nc8J5BJhkE3AP9oieECVpJ&index=5
    https://www.youtube.com/watch?v=hYrTh5Q8tIM&list=PLB9NsRTifc1nc8J5BJhkE3AP9oieECVpJ&index=6
    https://www.youtube.com/watch?v=hYrTh5Q8tIM&list=PLB9NsRTifc1nc8J5BJhkE3AP9oieECVpJ&index=7
    https://www.youtube.com/watch?v=hYrTh5Q8tIM&list=PLB9NsRTifc1nc8J5BJhkE3AP9oieECVpJ&index=8
    https://www.youtube.com/watch?v=hYrTh5Q8tIM&list=PLB9NsRTifc1nc8J5BJhkE3AP9oieECVpJ&index=9

