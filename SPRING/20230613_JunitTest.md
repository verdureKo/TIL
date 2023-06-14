# 테스트 코드

- 테스트의 필요성
    
    <aside>
    🔥 테스트는 무엇이고, 테스트가 필요한 이유는 무엇일까요?
    
    </aside>
    
    - 1) 개발은 어려운 일입니다.
        
        ![출처: [Programming Geeks](https://ko-kr.facebook.com/programminggeeks.in/photos/when-my-code-works-i/767945783344680/)](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/345b80b1-8aeb-4432-8eba-acc40dd3752e/Untitled.png)
        
        출처: [Programming Geeks](https://ko-kr.facebook.com/programminggeeks.in/photos/when-my-code-works-i/767945783344680/)
        
        - '버그' (bug) 란? (출처: [위키백과](https://ko.wikipedia.org/wiki/%EC%86%8C%ED%94%84%ED%8A%B8%EC%9B%A8%EC%96%B4_%EB%B2%84%EA%B7%B8))
            
            <aside>
            🤔 소프트웨어가 예상하지 못한 결과를 내는 것 입니다
            
            버그는 '**소스 코드'**나 '**설계과정에서의 오류'** 때문에 발생합니다.
            
            간혹 우리는 용어의 “정의”를 소홀히 하기도 하는데, 때로는 이렇게 용어를 다시 정리해보는 것 도 좋습니다. 버그라는 단어가 **“소프트웨어가 예상하지 못한 결과를 내는 것”** 이라는 정의를 가진다는것을 들으면 알겠지만, 듣지 않고도 정의를 정확히 말 할 수 없으면 우리가 테스트 코드를 작성하는 방법이 **“소프트웨어가 예상한대로 결과를 내는지 모든 상황을 체크해보기”** 라고 짐작하기 어렵겠죠?
            
            </aside>
            
        - '버그'가 얼마나 안좋은가요?
            
            <aside>
            🤔 또한 버그가 나쁘다는 것은 알지만 얼마나 나쁜지 와닿지 못하실 수 있습니다.
            특히 소비자 입장에서 무던하게 소프트웨어를 이용해오셨다면 특히 더 그렇겠죠?
            
            </aside>
            
            <aside>
            🙃 하지만 버그는….
            
            🥲 사용자에게 생각보다 큰 불편이나, 회사에 큰 악영향을 줍니다.
            
            🥲 일부 기능이 동작하지 않는데 그 일부 기능이 이커머스 사이트의 ‘주문’이라면?
            
            🥲 일부 기능이 의도와 다르게 동작하는데 그 기능이 이커머스 사이트의 ‘주문’이고, 10만원 결제건이 100만원이 결제되었다면?
            
            🥲 피크시간대에 회사의 서비스가 다운된다면?
            
            🥲 위와같은 일이 자주 일어나서 사용자들이 “이 사이트 이렇게 버그 많은데, 내 개인정보는 잘 보관하겠지?” 와 같은 의문을 가진다면?
            
            🙃 본격 개발자 호러쇼…
            
            </aside>
            
            <aside>
            🙃 심지어 건강한 우리와 다르게 소프트웨어는 시간이 지난다고 자동으로 치유되는 로직이 없습니다..
            
            </aside>
            
        
    - 2) 개발 코드 배포 전, 버그를 (최대한 많이) 찾아내는 법 - 테스트!
        - 1. 블랙박스 테스팅
            
            <aside>
            👉 블랙박스 테스팅이란 소프트웨어 내부 구조나 동작원리를 모르는 블랙박스와 같은 상태에서, 즉 웹 서비스의 사용자 입장에서 동작을 검사하는 방법입니다!
            
            </aside>
            
            1. 장점
                - 누구나 테스트가 가능합니다 - 개발자부터 디자이너, 베타 테스터 혹은 사장님까지!
                
            2. 단점
                - 기능이 증가될 수록 테스트의 범위가 증가합니다.
                    - 시간이 갈수록 테스트하는 사람이 계속 늘어나야함
                - 테스트 하는 사람에 따라 테스트 퀄러티가 다를 수 있습니다. → QA 직군이 있는 이유
                    
                    
        - 2. 개발자 테스트
            
            <aside>
            👉 개발자가 직접 "본인이 작성한 코드"를 검증하기 위해 "테스트 코드"를 작성합니다.
            
            </aside>
            
            1. 장점
                - 빠르고 정확한 테스트가 가능합니다. (예상 동작 VS 실제 동작)
                - 테스트 자동화가 가능합니다.
                    - 배포 절차 시 테스트 코드가 수행되어 동작 검증
                - 리팩토링이나 기능 추가를 할 때 더욱 편리합니다.
                
            2. 단점
                - 개발 시간이 오래 걸림
                - 테스트 코드를 유지보수하는 비용
                
    
    <aside>
    📌 Spring에서는 ****'테스트 코드' 작성을 잘 할 수 있는 환경을 제공 해줍니다.
    
    </aside>
    
- JUnit 사용 설정
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2ca3b9a1-e767-4d83-83e1-4b16d6f51441/Untitled.png)
    
    <aside>
    💡 JUnit이란 자바 프로그래밍 언어 용 단위 테스트 프레임워크입니다.
    
    </aside>
    
    ![Screen Shot 2023-05-11 at 5.45.37 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bfe69994-eaec-4876-8174-c280cf544760/Screen_Shot_2023-05-11_at_5.45.37_PM.png)
    
    - build.gradle 파일을 열어보면 JUnit 사용을 위한 환경설정이 이미 되어있습니다.
    
- 테스트 파일 생성
    - 계산기
        - [코드 스니펫] 계산기
            
            ```java
            package com.sparta.springprepare.calculator;
            
            public class Calculator {
                public Double operate(double num1, String op, double num2) {
                    switch (op) {
                        case "*":
                            return num1 * num2;
                        case "/":
                            if (num2 != 0) {
                                return num1 / num2;
                            } else {
                                return null;
                            }
                        case "+":
                            return num1 + num2;
                        case "-":
                            return num1 - num2;
                        default:
                            throw new IllegalArgumentException("잘못된 연산자입니다.");
                    }
                }
            }
            ```
            
        
    1. "Calculator.java" 파일 내에서 마우스 오른쪽 버튼 클릭 > **"Generate..."** 클릭
        
        ![Screen Shot 2023-05-11 at 6.40.21 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ef5ae562-07c6-4c39-ac3e-00f70434fd35/Screen_Shot_2023-05-11_at_6.40.21_PM.png)
        
    2. **"Test..."** 클릭
        
        ![Screen Shot 2023-05-11 at 6.40.34 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8325b20b-8f2b-4ee1-9bd3-440e457ba214/Screen_Shot_2023-05-11_at_6.40.34_PM.png)
        
    3. 기본세팅 그대로 OK 눌러서 생성
        
        ![Screen Shot 2023-05-11 at 6.40.52 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d9c495d3-056b-4986-8ce5-32bbaf1416a3/Screen_Shot_2023-05-11_at_6.40.52_PM.png)
        
        - 단축키 사용
            - Windows : `Ctrl` + `shift` + `t`
            - Mac : `⌘` + `shift` + `t`
            
        
        ![Screen Shot 2023-05-11 at 6.46.10 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/53b70c32-53bf-4393-a746-a432f571145b/Screen_Shot_2023-05-11_at_6.46.10_PM.png)
        
        - 위와 같이 자동으로 경로를 맞춰서 ‘CalculatorTest’ 파일이 생성된 것을 볼 수 있습니다.
        
- 테스트 코드 작성해보기!
    - [코드 스니펫] CalculatorTest
        
        ```java
        package com.sparta.springprepare.calculator;
        
        import org.junit.jupiter.api.Assertions;
        import org.junit.jupiter.api.DisplayName;
        import org.junit.jupiter.api.Test;
        
        class CalculatorTest {
            @Test
            @DisplayName("더하기 테스트")
            void test1() {
                Calculator calculator = new Calculator();
                Double result = calculator.operate(8, "+", 2);
                System.out.println("result = " + result);
        
                Assertions.assertEquals(10, result);
            }
        
            @Test
            @DisplayName("나누기 테스트")
            void test2() {
                Calculator calculator = new Calculator();
                Double result = calculator.operate(8, "/", 2);
                System.out.println("result = " + result);
        
                Assertions.assertEquals(4, result);
            }
        }
        ```
        
    - Java는 반드시 main() 메서드로 시작해 main() 메서드로 끝난다고 배우셨을 겁니다.
    - JUnit은 테스트 실행 환경을 가지고 있기 때문에 따로 main() 메서드를 실행하거나 서버를 실행시키지 않아도 이렇게 각각의 메서드 혹은 기능별로 테스트 코드를 작성하여 실행시킬 수 있습니다.
    - 더 자세한 내용은 이후 강의에서 다루겠습니다.
        