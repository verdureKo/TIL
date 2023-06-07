# 객체지향 프로그래밍_제네릭

## 01. # Chapter 13 : 🚰 모던 자바 알아보기 (람다, 스트림, Optional)

## 1. 모던 자바? : 자바 8 변경점 알아보기

- 프로그래밍 언어의 진화
    
    <aside>
    📌 자바는 진화하는 언어이며, 가장 큰 진화는 Java 8에서 이루어졌습니다.
    왜 진화해야하며, 어떤 진화를 했는지 아주 간단하게 살펴보려고 합니다.
    
    </aside>
    
    - 시장에서 프로그래머가 해결해야 하는 문제는 계속 변화합니다.
    - 문제가 변화하기 때문에, 프로그래밍 언어에 요구되는 기능들도 변화합니다.
    - 시대에 맞는 기능들을 제공하지 않는 언어들은 새로운 언어의 탄생을 야기합니다.
    - 새로운 언어가 탄생하고 해당 언어들이 프로덕션 레벨에 도달하는 동안 적응하지 못하면 해당 언어는 도태되기 시작합니다.
    - 예를들어 C/C++ 같은 언어들은 프로그램 실행에 대한 비용이 크지 않고, 하드웨어적인 보편성, 호환성에 큰 장점을 가지고 있었기 때문에 시장에서 가장 지배적인 입지를 차지했었습니다.
    - 하지만 특유의 난이도와 다른 요인들의 영향으로 예기치 않게 종료되거나, 보안 이슈가 많아지는 등 안정성이 떨어지게 됩니다.
    - 그러던 와중에 하드웨어는 꾸준한 진화를 거듭했고, 그 진화의 결과로 프로그램을 실행시키는 자원을 더 많이 사용해도 괜찮은 환경에서는, 더 안정성이 높은 c#, java와 같은 언어들이 각광받게 됩니다.
    - 물론 프로그래밍 언어의 장단점은 트레이드 오프를 가지기 때문에, 하나를 취하면 반대쪽의 하나를 내주게 되는 경우가 많고 위의 예시는 그러한 케이스 입니다 (성능-안정성)
    - 이처럼 시장의 상황에 따라서 프로그래밍 언어는 새로운 대안으로 등장하고, 적응해서 살아남거나, 적응하지 못해서 도태되기도 합니다.
    
    <aside>
    🤔 예시에 있는 c/c++이 도태된 언어냐고 하면 그건 절대 아닙니다. 아직도 성능이 매우 중요한 분야나, 아주 작은 컴퓨팅 파워만 가지고 있는 소형 하드웨어 쪽에서는 아직도 가장 메이저한 언어입니다. (물론 러스트라는 *~~환상적인~~*  언어의 위협을 받고 있지만요)
    
    다만 상향 평준화된 여러분의 컴퓨터나, 서버장비처럼 훌륭한 자원을 가지고 있는 환경에서는, 더 높은 안정성이 니즈에 부합했을 뿐이죠
    
    </aside>
    
- 자바의 대격변, Java 8
    - 자바의 시작
        
        <aside>
        📌 자바는 객체지향 프로그래밍이라는 소프트웨어 엔지니어링적인 이점을 가지고 있었고, jvm만 설치되어있다면, 어디서나 실행시킬 수 있다는 장점 때문에 크게 사랑받았습니다.
        
        </aside>
        
        - 자바는 객체지향 프로그래밍, 그 중에서도 캡슐화와 같은 장점을 가지고 있어서 프로그래머들의 생산성과 프로그램의 안정성을 가지고 있었습니다.
        - 그리고 초기의 c언어가 이식성이 높아서 사랑받았던 것처럼(다양한 하드웨어에서 최소한의 수정으로 c로 작성된 프로그램을 실행 시킬 수 있음), 자바 역시 jvm이 설치되어있는 환경이라면 프로그램을 실행 시킬 수 있었습니다.
        - 그 외에도 다양한 요인 덕에 웹 어플리케이션 시장에서 가장 사랑받는 언어중 하나로 거듭나게 되었습니다.
    - 자바가 직면했던 새로운 요구사항들
        
        <aside>
        📌 그러나 하드웨어의 진화와 새로운 요구사항의 탄생으로 자바 역시 새로운 생태계의 변화에 직면하게 되었습니다.
        
        </aside>
        
        - 1 - 병렬 처리
            - 간단하게만 언급하자면, 빅데이터를 처리할 필요성이 늘어났고, 멀티코어 컴퓨터와 같은 병렬 프로세싱이 가능한 장비들이 보급되면서 새로운 요구사항들이 생겨나게 됩니다.
            - 일단 당장은 병렬 처리와 같은 것들은 이런게 있다 정도만 알아주시면 됩니다. 오늘 다루는 범위는 람다와 스트림의 기능을 사용하거나, 해당 문법으로 작성된 코드를 이해할 수 있는 정도가 목표니까요
            - 만약 꼭 병렬처리가 어떠한 것인지 알고 싶으시다면 아래의 글을 읽어보는 것을 추천합니다.
                
                [재미로 읽어보는 ‘병렬처리’](https://medium.com/naver-cloud-platform/재미로-읽어보는-병렬처리-c60c8e3b62a7)
                
        - 2 - 함수형 프로그래밍
            
            <aside>
            📌 함수형 프로그래밍은, 객체 지향 프로그래밍처럼 프로그래밍의 패러다임의 한 종류 입니다.
            당연히 엄청나게 많은 공부가 필요하고, 여러분들은 지금 객체지향 프로그래밍을 배우는데 더 집중해야 합니다. 
            
            다만 자바8에서 새로운 문법이 도입된 이유를 알아보기 위해 아주 간단하게만 이야기 하고 넘어가려고 합니다.
            
            이해가 가지 않는다면, 과감하게 넘어가셔도 좋습니다.
            
            </aside>
            
            - 객체 지향 프로그래밍의 핵심 아이디어?
                1. 객체 지향 프로그래밍의 핵심 아이디어 자체는 간단합니다.
                    1. “프로그램을 객체들의 협력과 상호작용으로 바라보고 구현한다”  이죠
                2. 그 객체들을 정의하기 위해서 추상화와 같은 개념들을 사용 할 뿐 입니다.
                3. 핵심 개념을 통해서 달성하는 효용은 다음과 같습니다.
                    1. 코드의 재사용성이 높아진다.
                    2. 코드를 유지보수, 확장 하기 쉬워진다.
                    3. 코드를 신뢰성 있게 사용하기 쉬워진다. 
            - 함수형 프로그래밍의 핵심 아이디어?
                1. 함수형 프로그래밍의 핵심 아이디어 역시 간단합니다.
                    1. “수학의 함수처럼, 특정한 데이터에 의존하지 않고, 관련없는 데이터를 변경하지도 않으며, 결과값이 오직 입력값에만 영향을 받는 함수를 순수함수라고 합니다”
                        - 순수한 함수와 순수하지 못한 함수들
                            
                            ```java
                            // 수학의 함수
                            f(x, y) = x + 2xy
                            
                            // 순수한 메서드
                            // input에 따라 output은 항상 일정하죠!
                            public int someMethod(int x, int y) {
                            	return x + 2y;
                            }
                            
                            class notFunc {
                            	private int y = 0;
                            	private int result;
                            
                            	// 순수 메서드가 아닌 메서드
                            	// 메서드 안에서 제어할 수 없는 y라는 값에 의해 output이 바뀔 수 있죠
                            	public int anotherMethod(int x) {
                            		return x + this.y * 2;
                            	}
                            
                            	// 순수 메서드가 아닌 메서드 2
                            	// 메서드 내에서 this.result 값을 변경하고 반환하기 때문에
                            	// 순수 메서드라고 보기는 어렵습니다!
                            	public int otherMethod(int x, int y) {
                            		int result = x + 2 * y;
                            		this.result = result;
                            		return result;
                            	}
                            }
                            ```
                            
                    2. 프로그램을 순수한 함수의 모음으로 바라보고 구현한다 입니다.
                2. 핵심 개념을 통해서 달성하는 효용은 다음과 같습니다.
                    1. 검증이 쉽다 (검증이 필요한 부분만 검증 할 수 있음)
                    2. 성능 최적화가 쉽다 (특정 input에 대한 output을 재사용 할 수 있음 - 캐싱)
                    3. 동시성 문제를 해결하기 쉽다 (함수는 다른 값의 변경을 야기하지 않음)
        - 가장 중요하지만, 가장 쉬운 결론
            
            <aside>
            🤔 아무튼 자바는 처음에는 잘 해와서 기존언어의 자리를 차리하며 거대하게 성장했지만, 새로운 생태계에 맞는 요구사항이 발생하면서, 진화하거나 도태되거나 하는 시점에 도달했다는 것 입니다.
            
            </aside>
            
    - 결론 : Java 8에서 새롭게 추가된 개념들
        - 자바 함수의 변화
            
            <aside>
            🤔 결국 자바 함수형 프로그래밍의 기능들을 추가하기로 결정합니다.
            
            </aside>
            
            - 함수형 프로그래밍 아이디어 1 : 함수를 일급 값으로
                1. 우리가 지금까지 배웠던 자바에서 “조작할 수 있는”값은 다음과 같습니다.
                    1. 기본값 (int, long, bollean, …)
                    2. 객체
                2. 1-a, 1-b 와 같은 값들은 다음과 같은 특징을 같습니다.
                    1. 함수에 인자로 넘길 수 있다.
                    2. 함수의 결과로 반환 할 수 있다.
                    3. 값을 수정할 수 있다
                    4. 값을 변수에 대입할 수 있다.
                3. 사실상 프로그래밍에서 지원하는 모든 연산을 지원하고 있고, 이러한 연산을 모두 지원하는 “값”들을 일급 시민, 또는 일급 객체라고 합니다.
                4. 그러나 메서드는 어떤가요?
                    1. 메서드에 인자로 메서드를 넘길 수 있나요?
                    2. 메서드의 결과로 메서드를 반환 할 수 있나요?
                    3. 메서드를 변수에 대입 할 수 있나요?
                5. 특정한 연산을 지원하지 않는 값이기 때문에 메서드는 이급 시민으로 볼 수 있습니다.
                6. 그렇지만 함수를 값으로 취급 할 수 있다면 매우 많은 것들을 할 수 있고, 함수형 프로그래밍에서는 이를 적극 이용해 오고 있었습니다.
                
                <aside>
                📌 결론 : Java 8에 메서드 참조 기능이 도입되었습니다.
                
                </aside>
                
            - 함수형 프로그래밍 아이디어 2 : 람다: 익명함수
                - 람다는 익명함수를 지칭하는 말 입니다.
                - 익명함수란 말 그대로 이름이 없는 함수를 뜻하며, 일급 객체로 취급됩니다.
                - 함수를 값으로 사용 할 수도 있으며 파라미터에 전달 하기
                - 변수에 대입 하기와 같은 연산들이 가능합니다.
                - 자세한 문법은 아래에서 다시 소개 할 예정입니다.
        - 스트림
            1. 스트림은 데이터 처리연산을 지원하도록 소스에서 추출된 연속된 요소입니다.
            2. 컬렉션이 데이터를 저장하거나 접근하는데 초점을 맞춘 인터페이스라면
            3. 스트림은 데이터를 처리하는데 초점을 맞춘 인터페이스입니다.
            4. 이해가 가지 않는다면, 일단 컬렉션의 반복을 멋지게 처리하는 일종의 기능이자, 멀티스레드 관련 코드를 구현하지 않아도 알아서 병렬로 추가해주는 기능이라고 생각하시면 좋습니다.
        - 너무 어려워요..(요약!)
            
            <aside>
            📌 물론 한 주차만에, 람다와 스트림의 모든 개념과 구현을 이해 할 수 없습니다. 
            
            이번 강의의 현실적인 목표는 자주 사용되는 람다와 스트림 문법을 이해하기, 
            사용하기 입니다.
            
            그 관점에서 위의 내용은 단순히 용어 정리 이며, 직접 “이게 왜 가능하지?”를 알아보고 싶으신 분들을 위한 실마리라고 생각해주시면 좋을 것 같습니다.
            
            그래도 꼭 인지하고 가셔야 할 요약 내용은 다음과 같습니다.
            
            </aside>
            
            1. 함수형 프로그래밍의 아이디어와 문법을 자바8에서 지원한다.
            2. 함수형 프로그래밍의 아이디어인 (함수를 값으로 다루거나, 다른 함수에 넘길 수 있다)와 같은 일들이 가능하다.
            3. 함수형 프로그래밍의 문법인 익명함수 문법을 지원한다.
            4. 스트림이라는 컬렉션의 흐름과 같은 것을 지원한다.
            5. 스트림 기능의 지원으로 우리는 더 간결하고, 유연하고, 성능좋은 코드를 작성 할 수 있다.
            

## 2. 람다와 스트림 문법 살펴보기

- 람다와 스트림을 적용할 예시코드
    
    ```java
    import java.util.ArrayList;
    import java.util.List;
    
    public class LambdaAndStream {
        public static void main(String[] args) {
            ArrayList<Car> carsWantToPark = new ArrayList<>();
            ArrayList<Car> parkingLot = new ArrayList<>();
    
            Car car1 = new Car("Benz", "Class E", true, 0);
            Car car2 = new Car("BMW", "Series 7", false, 100);
            Car car3 = new Car("BMW", "X9", false, 0);
            Car car4 = new Car("Audi", "A7", true, 0);
            Car car5 = new Car("Hyundai", "Ionic 6", false, 10000);
    
            carsWantToPark.add(car1);
            carsWantToPark.add(car2);
            carsWantToPark.add(car3);
            carsWantToPark.add(car4);
            carsWantToPark.add(car5);
    
            parkingLot.addAll(parkingCarWithTicket(carsWantToPark));
            parkingLot.addAll(parkingCarWithMoney(carsWantToPark));
    
            for (Car car : parkingLot) {
                System.out.println("Parked Car : " + car.getCompany() + "-" + car.getModel());
            }
    
        }
    
        public static List<Car> parkingCarWithTicket(List<Car> carsWantToPark) {
            ArrayList<Car> cars = new ArrayList<>();
            
            for (Car car : carsWantToPark) {
                if (car.hasParkingTicket()) {
                    cars.add(car);
                }
            }
    
            return cars;
        }
    
        public static List<Car> parkingCarWithMoney(List<Car> carsWantToPark) {
            ArrayList<Car> cars = new ArrayList<>();
            
            for (Car car : carsWantToPark) {
                if (!car.hasParkingTicket() && car.getParkingMoney() > 1000) {
                    cars.add(car);
                }
            }
            
            return cars;
        }
    }
    
    class Car {
        private final String company; // 자동차 회사
        private final String model; // 자동차 모델
    
        private final boolean hasParkingTicket;
        private final int parkingMoney;
    
        public Car(String company, String model, boolean hasParkingTicket, int parkingMoney) {
            this.company = company;
            this.model = model;
            this.hasParkingTicket = hasParkingTicket;
            this.parkingMoney = parkingMoney;
        }
    
        public String getCompany() {
            return company;
        }
    
        public String getModel() {
            return model;
        }
    
        public boolean hasParkingTicket() {
            return hasParkingTicket;
        }
    
        public int getParkingMoney() {
            return parkingMoney;
        }
    }
    ```
    
- 함수를 값으로 전달하기 : 함수형 인터페이스
    - 함수를 값으로 전달하려면 어떻게 해야할까요?
    - 일단 메소드에 파라미터를 전달하는 경우를 생각해볼까요?
    
    ```java
    // 음.. ??? 에 무엇을 넣어야 할까요?
    public exampleMethod(int parameter1, ??? parameterFunction) { ... }
    ```
    
    - 🤔 : 일단 타입을 정의해줘야겠네요..
    - 이럴때 사용하는 것이 함수형 인터페이스 입니다.
    - 인터페이스가 타입 역할을 하는건 기억나시죠?
    - 함수를 전달할때 타입을 알려주기 위해서 함수형 인터페이스를 선언하거나 사용해야 합니다.
    - 함수형 인터페이스는 다음과 같은 특징을 가지고 있습니다.
        - 추상 메소드를 딱 하나만 가지고 있는 인터페이스
        - @FunctionalInterface 어노테이션으로 검증 할 수 있음
    - 그러면 함수형 인터페이스와 함수를 값으로 전달하기 위해서 값으로 전달할 함수를 먼저 만들어 볼까요?
        
        ```java
        // Car 클래스 내부에 두 메서드 구현
        
        public static boolean hasTicket(Car car) {
                return car.hasParkingTicket;
        }
        
        public static boolean noTicketButMoney(Car car) {
                return !car.hasParkingTicket && car.getParkingMoney() > 1000;
        }
        ```
        
    - 함수형 인터페이스를 다음과 같이 정리합니다.
        
        ```java
        interface Predicate<T> {
            boolean test(T t);
        }
        ```
        
    - 이 두 함수를 리팩토링 해볼까요?
        
        ```java
        public static List<Car> parkingCarWithTicket(List<Car> carsWantToPark) {
                ArrayList<Car> cars = new ArrayList<>();
        
                for (Car car : carsWantToPark) {
                    if (car.hasParkingTicket()) {
                        cars.add(car);
                    }
                }
        
                return cars;
          }
        
        public static List<Car> parkingCarWithMoney(List<Car> carsWantToPark) {
            ArrayList<Car> cars = new ArrayList<>();
        
            for (Car car : carsWantToPark) {
                if (!car.hasParkingTicket() && car.getParkingMoney() > 1000) {
                    cars.add(car);
                }
            }
        
            return cars;
        }
        ```
        
    - 우리는 함수를 값으로 처리 할 수 있게 됐기 때문에, 거의 똑같은 두개의 함수 따위는 필요가 없습니다.
    - 우리의 새로운 함수 입니다.
        
        ```java
        // 변경점 1 : Predicate<Car> 인터페이스를 타입 삼아 함수를 전달합니다!
        public static List<Car> parkCars(List<Car> carsWantToPark, Predicate<Car> function) {
              List<Car> cars = new ArrayList<>();
        
              for (Car car : carsWantToPark) {
        					// 변경점 2 : 전달된 함수는 다음과 같이 사용됩니다!
                  if (function.test(car)) {
                      cars.add(car);
                  }
              }
        
              return cars;
          }
        ```
        
    - 실제로 어떻게 사용하는지 볼까요?
        
        ```java
        parkingLot.addAll(parkCars(carsWantToPark, Car::hasTicket));
        parkingLot.addAll(parkCars(carsWantToPark, Car::noTicketButMoney));
        ```
        
        - 새로운 문법 Car::hasTicket 이 보이시나요?
        - 우리는 함수를 값으로 취급하기 때문에, 함수를 참조로 불러서 쓸 수 있습니다.
        - Car 클래스의 hasTicket 함수를 값으로 가져와서 전달하는 부분입니다!
    - 함수를 값으로 전달 리팩토링 완료 코드
        
        ```java
        import java.util.ArrayList;
        import java.util.List;
        
        public class LambdaAndStream {
            public static void main(String[] args) {
                ArrayList<Car> carsWantToPark = new ArrayList<>();
                ArrayList<Car> parkingLot = new ArrayList<>();
        
                Car car1 = new Car("Benz", "Class E", true, 0);
                Car car2 = new Car("BMW", "Series 7", false, 100);
                Car car3 = new Car("BMW", "X9", false, 0);
                Car car4 = new Car("Audi", "A7", true, 0);
                Car car5 = new Car("Hyundai", "Ionic 6", false, 10000);
        
                carsWantToPark.add(car1);
                carsWantToPark.add(car2);
                carsWantToPark.add(car3);
                carsWantToPark.add(car4);
                carsWantToPark.add(car5);
        
                parkingLot.addAll(parkCars(carsWantToPark, Car::hasTicket));
                parkingLot.addAll(parkCars(carsWantToPark, Car::noTicketButMoney));
        
                for (Car car : parkingLot) {
                    System.out.println("Parked Car : " + car.getCompany() + "-" + car.getModel());
                }
        
            }
        
            public static List<Car> parkCars(List<Car> carsWantToPark, Predicate<Car> function) {
                List<Car> cars = new ArrayList<>();
        
                for (Car car : carsWantToPark) {
                    if (function.test(car)) {
                        cars.add(car);
                    }
                }
        
                return cars;
            }
        
        }
        
        class Car {
            private final String company; // 자동차 회사
            private final String model; // 자동차 모델
        
            private final boolean hasParkingTicket;
            private final int parkingMoney;
        
            public Car(String company, String model, boolean hasParkingTicket, int parkingMoney) {
                this.company = company;
                this.model = model;
                this.hasParkingTicket = hasParkingTicket;
                this.parkingMoney = parkingMoney;
            }
        
            public String getCompany() {
                return company;
            }
        
            public String getModel() {
                return model;
            }
        
            public boolean hasParkingTicket() {
                return hasParkingTicket;
            }
        
            public int getParkingMoney() {
                return parkingMoney;
            }
        
            public static boolean hasTicket(Car car) {
                return car.hasParkingTicket;
            }
        
            public static boolean noTicketButMoney(Car car) {
                return !car.hasParkingTicket && car.getParkingMoney() > 1000;
            }
        }
        
        interface Predicate<T> {
            boolean test(T t);
        }
        ```
        
    
- 람다: 익명함수로 함수 한 번 간단하게 사용하기
    
    <aside>
    🤔 음… 주말이라 주차장은 꽉 차 있는데, 주차 티켓이 있다고 해서 날로먹는게 꼴보기 싫네요..
    주말에는 돈도 있고 티켓도 있어야 주차가 가능하다고 정책을 새로 새워볼까요?
    근데 주말에 한 번 사용하고 말건데, 메소드로 구현하기가 너무 귀찮네요..
    
    </aside>
    
    - 이럴 땐 람다 익명함수를 이용하면 됩니다!
        
        ```java
        // 주말의 주차장 추가
        ArrayList<Car> weekendParkingLot = new ArrayList<>();
        
        weekendParkingLot
        .addAll(parkCars(carsWantToPark, (Car car) -> car.hasParkingTicket() && car.getParkingMoney() > 1000));
        ```
        
        - 새로운 문법! (Car car) -> car.hasParkingTicket() && car.getParkingMoney() > 1000))
        - 함수를 값으로 전달하는데, 어딘가에 구현하지 않고 그냥 간단하게 구현해서 넘기고 싶으면 람다식을 이용하면 됩니다!
        - 람다식은 “함수 값”으로 평가되며, 한번만 사용됩니다.
        - 문법도 그만큼 간결하게 작성할 수 있습니다.
        - 람다 함수 문법
            
            ```java
            // 기본적으로 문법은 다음과 같습니다.
            (파라미터 값, ...) -> { 함수 몸체 }
            
            // 아래의 함수 두개는 같은 함수입니다.
            // 이름 반환타입, return문 여부에 따라 {}까지도 생략이 가능합니다.
            public int toLambdaMethod(int x, int y) {
            	return x + y;
            }
            
            (x, y) -> x + y
            
            // 이런 함수도 가능하겠죠?
            public int toLambdaMethod2() {
            	return 100;
            }
            
            () -> 100
            
            // 모든 유형의 함수에 가능합니다.
            public void toLambdaMethod3() {
            	System.out.println("Hello World");
            }
            
            () -> System.out.println("Hello World")
            ```
            
            - 사실 이게 거의 전부이지만 조금 더 세세한 문법은 아래의 링크에서 확인 가능합니다.
            
            [코딩교육 티씨피스쿨](http://www.tcpschool.com/java/java_lambda_concept)
            
        - 추가 완료 코드
            
            ```java
            import java.util.ArrayList;
            import java.util.List;
            
            public class LambdaAndStream {
                public static void main(String[] args) {
                    ArrayList<Car> carsWantToPark = new ArrayList<>();
                    ArrayList<Car> parkingLot = new ArrayList<>();
                    ArrayList<Car> weekendParkingLot = new ArrayList<>();
            
                    Car car1 = new Car("Benz", "Class E", true, 0);
                    Car car2 = new Car("BMW", "Series 7", false, 100);
                    Car car3 = new Car("BMW", "X9", false, 0);
                    Car car4 = new Car("Audi", "A7", true, 0);
                    Car car5 = new Car("Hyundai", "Ionic 6", false, 10000);
            
                    carsWantToPark.add(car1);
                    carsWantToPark.add(car2);
                    carsWantToPark.add(car3);
                    carsWantToPark.add(car4);
                    carsWantToPark.add(car5);
            
                    parkingLot.addAll(parkCars(carsWantToPark, Car::hasTicket));
                    parkingLot.addAll(parkCars(carsWantToPark, Car::noTicketButMoney));
            
                    weekendParkingLot.addAll(parkCars(carsWantToPark, (Car car) -> car.hasParkingTicket() && car.getParkingMoney() > 1000));
            
                    for (Car car : parkingLot) {
                        System.out.println("Parked Car : " + car.getCompany() + "-" + car.getModel());
                    }
            
                }
            
                public static List<Car> parkCars(List<Car> carsWantToPark, Predicate<Car> function) {
                    List<Car> cars = new ArrayList<>();
            
                    for (Car car : carsWantToPark) {
                        if (function.test(car)) {
                            cars.add(car);
                        }
                    }
            
                    return cars;
                }
            
            }
            
            class Car {
                private final String company; // 자동차 회사
                private final String model; // 자동차 모델
            
                private final boolean hasParkingTicket;
                private final int parkingMoney;
            
                public Car(String company, String model, boolean hasParkingTicket, int parkingMoney) {
                    this.company = company;
                    this.model = model;
                    this.hasParkingTicket = hasParkingTicket;
                    this.parkingMoney = parkingMoney;
                }
            
                public String getCompany() {
                    return company;
                }
            
                public String getModel() {
                    return model;
                }
            
                public boolean hasParkingTicket() {
                    return hasParkingTicket;
                }
            
                public int getParkingMoney() {
                    return parkingMoney;
                }
            
                public static boolean hasTicket(Car car) {
                    return car.hasParkingTicket;
                }
            
                public static boolean noTicketButMoney(Car car) {
                    return !car.hasParkingTicket && car.getParkingMoney() > 1000;
                }
            }
            
            interface Predicate<T> {
                boolean test(T t);
            }
            ```
            
        
- 스트림 알아보기
    
    <aside>
    📌 스트림은 정확하게는 Java 8부터 제공되는, 한번 더 추상화된 자료구조와 자주 사용하는 프로그래밍 API를 제공한 것 입니다. 자료구조를 한 번 더 추상화 했기 때문에, 자료구조의 종류에 상관 없이 같은 방식으로 다룰 수 있습니다.
    ( + 병렬 처리에 유리한 구조로 조건부로 성능도 챙길 수 있습니다.)
    
    조금 더 쉽게 “비유”하자면, 자료구조의 “흐름”을 객체로 제공해주고, 그 흐름동안 사용할 수 있는 메서드들을 api로 제공해주고 있는 것이죠
    
    일단은 “자료구조” (리스트, 맵, 셋 등)의 흐름이라고 비유하면 이해가 조금 더 쉬울 것 같습니다.
    
    </aside>
    
    - 스트림의 특징
        1. 원본의 데이터를 변경하지 않습니다.
            1. 자바 컬렉션으로부터 스트림(해당 컬렉션의 흐름)을 받아서 한 번 사용합니다.
        2. 일회용입니다.
            1. 한 번 사용한 스트림은 어디에도 남지 않습니다.
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fed496eb-0b68-4bf9-8b12-7102c729fb84/Untitled.png)
        
        <aside>
        🤔 위는 java.collection 내부의 stream()메서드 입니다.
        아직은 잘 모르겠는 스트림을 반환합니다.
        collection에 정의되어있기 때문에, 
        모든 컬렉션을 상속하는 구현체들은 스트림을 반환 할 수 있습니다.
        
        </aside>
        
    - 스트림과 거기에 구현되어 있는 메서드를 이용하면 다음과 같은 것들이 가능합니다.
        
        ```java
        List<Car> benzParkingLot =
        								// carsWantToPark의 스트림값을 받아와서
                        carsWantToPark.stream()
        												// 거기 구현되어 있는 filter()메서드를 사용합니다.
        												// filter메서드는 함수를 파라미터로 전달받습니다.
        												// 여기서 함수는 제조사가 벤츠면 true를 반환하는 함수네요.
        												// 필터 메서드는 이름처럼 false를 반환한 스트림의 원소들을 제거합니다.
                                .filter((Car car) -> car.getCompany().equals("Benz"))
        												// 이 결과도 반환을 받아서 다시 리스트로 묶어줍니다.
                                .toList();
        ```
        
        - 위의 로직을 정리해보면
            1. 스트림 객체를 받습니다.
            2. 해당 객체는 자료구조의 모든 원소가 있습니다.
            3. filter()와 같은 이미 구현된 메소드도 있습니다.
            4. filter() 메소드는 true/false 값을 return하는 함수를 파라미터로 전달받습니다.
            5. filter() 메소드는 스트림에 들어있는 모든 원소에 파라미터로 전달받은 함수를 실행시켜보면서 (우리의 코드 같은 경우 모든 원소가 익명함수의 Car car 파라미터로 자동으로 전달됩니다.)
            6. false가 나온 원소를 제거한 스트림을 반환해줍니다.
            7. 해당 결과를 다시 컬렉션으로 묶어주는 메서드도 정의되어있습니다.
        - 사실 간단하게는 다음과 같은 일을 하고 있는 것이죠
            
            ```java
            ArrayList<Car> benzParkingLotWithoutStream = new ArrayList<>();
            
            for (Car car : carsWantToPark) {
                if (car.getCompany().equals("Benz")) {
                    benzParkingLotWithoutStream.add(car);
                }
            }
            ```
            
    - 스트림을 사용하는 방법
        1. 스트림을 받아오기 (.stream())
            
            ```java
            carsWantToPark.stream()
            ```
            
        2. 스트림 가공하기
            
            ```java
            .filter((Car car) -> car.getCompany().equals("Benz"))
            ```
            
        3. 스트림 결과 만들기
            
            ```java
            .toList();
            ```
            
    - 스트림 API
        
        <aside>
        📌 스트림 api는 너무 방대해서 한번에 다 소개할수도, 배울수도 없습니다.
        코드를 마주 할 때 마다, 혹은 사용해보면서 어떤 것들이 있는지 알아보는것이 중요합니다.
        
        </aside>
        
        - 그래도 가장 대표적인 api인 map(), forEach(), filter() 정도는 가장 자주 사용되기 때문에 꼭 확인하고 넘어가면 좋을 것 같습니다.
        - forEach()
            
            ```java
            List<String> carNames = Arrays.asList("Series 6", "A9", "Ionic 6");
            
            carNames.stream()
                .forEach(System.out::println);
            
            // 결과 
            // Series 6
            // A9
            // Ionic 6
            ```
            
            - 각각의 원소에 넘겨받은 함수를 실행해줍니다.
            - 하지만 넘겨받은 반환값을 가지고 뭘 하지는 않으며, 있다고 해도 무시됩니다.
        - map()
            
            ```java
            carNames.stream()
            	.map(name -> name.toUpperCase()).toList();
            
            // 결과
            // ["SERIES 6", "A9", "IONIC 6"]
            ```
            
            - forEach와는 반대로 넘겨받은 토대로 값을 변환시키는데 주로 사용됩니다.
        - 나머지 스트림 Api들도 정말 유용한 것들이 많습니다. 다만 지금은 map, filter, foreach정도와 결과를 가져오는 몇가지 코드만 이해하고 넘어가는게 좋을 것 같습니다.
        - 아래의 링크에서 다양한 Stream Api들을 확인 할 수 있습니다.
            
            [](https://www.baeldung.com/java-8-streams)
            
        
    

## 3.  Null은 10억 달러 짜리 실수다? Optional

- null은 나쁘다?
    - null은 Tony Hoare가 만든 개념입니다.
    - 기본적으로 아무것도 참조하지 않는다는 것을 의미합니다.
    - 2009년에 Tony Hoare는 null이라는 개념을 만든것이 1조원짜리 실수라고 이야기 했습니다.
    - 자세한 이야기는 아래의 링크에 있지만, 매우 간략하게 요약하자면
        - null이라는 “개념”이 존재하기 때문에, 거의 모든 상황에 null이 발생 할 수 있음을 경계해야 합니다.
        - 이상적이라면 모두가 메서드 이름을 “findWhateverAndIfNoExistReturnNull()” 처럼 작성하고
        - 해당메서드를 사용하는 모두는 null 체크를 해줘야겠죠
        - 하지만 그런일은 일어나지 않았고, 이것을 가리켜 10억 달러짜리 실수라고 밝혔습니다.
            
            [왜 Null을 보고 나쁘다고 하는걸까?](https://zorba91.tistory.com/339)
            
- null이 나쁜 케이스
    
    <aside>
    📌 다음과 같은 코드는 초보자들이 자주 하는 실수이며, null이 왜 위험한지를 단적으로 보여주는 예시입니다.
    
    </aside>
    
    ```java
    public class NullIsDanger {
        public static void main(String[] args) {
    
            SomeDBClient myDB = new SomeDBClient();
            
            String userId = myDB.findUserIdByUsername("HelloWorldMan");
    
            System.out.println("HelloWorldMan's user Id is : " + userId);
        }
    }
    
    class SomeDBClient {
    
        public String findUserIdByUsername(String username) {
            // ... db에서 찾아오는 로직
    				String data = "DB Connection Result";
    
            if (data != null) {
                return data;
            } else {
                return null;
            } 
        }
        
    }
    ```
    
    - 개선 1 : 위 코드의 문제점
        1. 논리적으로도, 환경적으로도 null이 반환될 여지가 있음에도, null이 반환될 수 있음을 명시하지 않았습니다.
        2. 메인함수쪽에서, 사용 할 때 null체크를 하지 않아, 만약 null이 반환된다면, nullPointerException이 발생하게 됩니다.
        - 개선 1 : null이 반환될 여지를 명시하고, 그 메서드를 사용하는 사람이 조심하기
            
            ```java
            public class NullIsDanger {
                public static void main(String[] args) {
            
                    SomeDBClient myDB = new SomeDBClient();
            
                    String userId = myDB.findUserIdByUsernameOrThrowNull("HelloWorldMan");
                    // 개선 1: null이 반환 될 수 있음을 인지한 메서드 사용자는, null을 대비합니다.
                    if (userId != null) {
                        System.out.println("HelloWorldMan's user Id is : " + userId);
                    }
                }
            }
            
            class SomeDBClient {
                // 개선 1: 이 메서드는 null이 반환 될 수 있음을 명시합니다.
                public String findUserIdByUsernameOrThrowNull(String username) {
                    // ... db에서 찾아오는 로직
            				String data = "DB Connection Result";
            
                    if (data != null) {
                        return data;
                    } else {
                        return null;
                    }
                }
            
            }
            ```
            
    - 개선 2 : 개선 1의 문제점
        
        <aside>
        🤔 약속은 깨지라고 있는 것이고, 사람은 실수하게 되어 있습니다.
        누군가는 바빠서, 혹은 익숙하지 않아서 null체크를 하지 않는다면 시스템은 위험에 빠집니다.
        
        </aside>
        
        - 개선 2 : 객체를 감싸서 반환하기
            
            ```java
            // 개선 2: 결과값을 감싼 객체를 만듭니다.
            class SomeObjectForNullableReturn {
                private final String returnValue;
                private final Boolean isSuccess;
            
                SomeObjectForNullableReturn(String returnValue, Boolean isSuccess) {
                    this.returnValue = returnValue;
                    this.isSuccess = isSuccess;
                }
            
                public String getReturnValue() {
                    return returnValue;
                }
            
                public Boolean isSuccess() {
                    return isSuccess;
                }
            }
            
            public class NullIsDanger {
                public static void main(String[] args) {
            
                    SomeDBClient myDB = new SomeDBClient();
            
                    // 개선 2 : 이제 해당 메서드를 사용하는 유저는, 객체를 리턴받기 때문에 더 자연스럽게 성공여부를 체크하게 됩니다.
                    SomeObjectForNullableReturn getData = myDB.findUserIdByUsername("HelloWorldMan");
            
                    if (getData.isSuccess()) {
                        System.out.println("HelloWorldMan's user Id is : " + getData.getReturnValue());
                    }
                }
            }
            
            class SomeDBClient {
                // 개선 2 : 결과값을 감싼 객체를 리턴합니다.
                public SomeObjectForNullableReturn findUserIdByUsername(String username) {
                    // ... db에서 찾아오는 로직
                    String data = "DB Connection Result";
            
                    if (data != null) {
                        return new SomeObjectForNullableReturn(data, true);
                    } else {
                        return new SomeObjectForNullableReturn(null, false);
                    }
                }
            
            }
            ```
            
            - 이제 해당 메서드는 결과를 감싼 객체를 리턴하고
            - 감싼 객체를 리턴받은 유저는 이 메서드가 위험할 수 있다는 것을 더 쉽게 인지 할 수 있습니다.
            
        
    - 개선 3 : 개선 2의 아이디어 발전시키기
        
        ```java
        class SomeObjectForNullableReturn<T> {
            private final T returnValue;
            private final Boolean isSuccess;
           
            
        
            SomeObjectForNullableReturn(T returnValue, Boolean isSuccess) {
                this.returnValue = returnValue;
                this.isSuccess = isSuccess;
            }
        
            public T getReturnValue() {
                return returnValue;
            }
        
            public Boolean isSuccess() {
                return isSuccess;
            }
            
        }
        ```
        
        - “감싸는 객체”를 조금 수정하면, 이제 위험 할 수 있는 모든 메서드에 사용 할 수 있게 됩니다.
    - 결론 : 개선 3의 아이디어를 발전시킨것이 java.util.Optional 객체 입니다.
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/50f7c395-623a-4867-81e6-7fb657ca4955/Untitled.png)
        
        - 실제 java.util.Optional 객체의 소스코드입니다.
        - 우리가 데이터를 감싸면서 했던 로직들과, 그 외에도 처리를 편하게 해주는 로직들이 있습니다.
- 지금부터라도 잘하자! Optional<T>
    - Optional 기본 정리
        - Java8에서는 Optional<T> 클래스를 사용해 Null Pointer Exception을 방지할 수 있도록 도와줍니다.
        - Optional<T>는 null이 올 수 있는 값을 감싸는 Wrapper 클래스입니다.
        - Optional이 비어있더라도, 참조해도 Null Pointer Exception가 발생하지 않습니다.
    - Optional 간단 사용법
        - 값이 null 인 Optional 생성하기
            
            ```java
            Optional<Car> emptyOptional = Optional.empty();
            ```
            
        - 값이 있는 Optional 생성하기
            
            ```java
            Optional<Car> hasDataOptional = Optional.of(new Car());
            ```
            
        - 값이 있을수도 없을수도 있는 Optional 생성하기
            
            ```java
            Optional<Car> hasDataOptional = Optional.ofNullable(getCarFromDB());
            ```
            
        - Optional 객체 사용하기 (값 받아오기)
            
            ```java
            Optional<String> carName = getCarNameFromDB();
            // orElse() 를 통해 값을 받아옵니다, 파라미터로는 null인 경우 반환할 값을 적습니다.
            String realCarName = carName.orElse("NoCar");
            
            // 위는 예시코드고 실제는 보통 아래와 같이 사용하겠죠?
            String carName = getCarNameFromDB().orElse("NoCar");
            
            // orElseGet()이라는 메서드를 사용해서 값을 받아올 수 있습니다.
            // 파라미터로는 없는 경우 실행될 함수를 전달합니다.
            Car car = getCarNameFromDB().orElseGet(Car::new);
            
            // 값이 없으면, 그 아래 로직을 수행하는데 큰 장애가 되는경우 에러를 발생시킬수도 있습니다.
            Car car = getCarNameFromDB()
            						.orElseThrow(() -> new CarNotFoundException("NO CAR!)
            ```
            