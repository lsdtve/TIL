# 함수형 인터페이스

- **추상 메소드**를 딱 하나만 가지고 있는 인터페이스

- **Single Abstract Method** 인터페이스
- `@FuncationInterface` 애노테이션을 가지고 있는 인터페이스



### 기본 함수형 인터페이스

1. **Function<T, R>**
   - T타입을 받아서 R타입을 리턴하는 함수 인터페이스
     - R apply(T t)
   - 함수 조합용 메소드
     - andThen
     - compose
2. **BiFunction<T, U, R>**
   - 두 개의 값(T,U)를 받아서 R타입을 리턴하는 함수 인터페이스
     - R apply(T t, U u)
   - 함수 조합용 메소드
     - andThan
3. **Comsumer<T>**
   - T 타입을 받아서 아무값도 리턴하지 않는 함수 인터페이스
     - void Accept(T t)
   - 함수 조합용 메소드
     - andThan
4. **Supplier<T>**
   - T타입의 값을 제공하는 함수 인터페이스
     - T get()
5. **Predicate<T>**
   - T타입을 받아서 boolean을 리턴하는 함수 인터페이스
     - boolean test(T t)
   - 함수 조합용 메소드
     - And, Or, Negate
6. **UnaryOperator<T>**
   - Function<T, R>의 특수한 형태로,  입력값 하나를 받아서 동일한 타입을 리턴하는 함수 인터페이스
7. **BinaryOperator<T>**
   - BiFunction<T, U, R>의 특수한 형태로, 동일한 타입의 입력값 두개를 받아 리턴하는 함수 인터페이스



# Lambda

- Lambda는 메소드를 하나의 식으로 표현하는 것이다.
- 익명 메소드 생성 문법이라 할 수 있다.



### 람다 기본식

```text
람다의 기본식 : (매개변수) -> {실행문}

인자가 없을 때  : () -> {실행문}
인자가 한개일 때  : (one) -> {실행문}
							   one  -> {실행문}
인자가 여러개 일 때 : (one, two) -> {실행문}
```

  인자 타입은 생략 가능하다.



### 메소드 레퍼런스

- 메소드 레퍼런스를 사용해서 매우 간결하게 표현할 수 있다.

1. **스태틱 메소드 참조**

   ```java
   // 타입::스테틱 메소드
   public class Member {
     static String hello(String name) {
       return "hello " + name;
     }
   }
   
   public class Main {
     public static void main(String[] args) {
       UnaryOperator<String> op = Member::hello;
   
       System.out.println(op.apply("bae"));
     }
   }
   ```

2. **특정 객체의 인스턴스 메소드 참조**

   ```java
   // 타입::스테틱 메소드
   public class Member {
       public String hello(String name) {
           return "hello " + name;
       }
   }
   
   public class Main {
       public static void main(String[] args) {
           Member member = new Member();
           UnaryOperator<String> hello = member::hello;
       }
   }
   ```
   

   
3. **임의 객체의 인스턴스 메소드 참조**

   ```java
   // 타입::인스턴스 메소드
   public class Main {
       public static void main(String[] args) {
           String[] names = {"kim","bae","su"};
           Arrays.sort(names, String::compareToIgnoreCase);
       }
   }
   ```


4. **생성자 참조**

   ```java
   // 타입::new
   public class Member {
       public Member() {}
   }
   
   public class Main {
       public static void main(String[] args) {
           Supplier<Member> newMember = Member::new;
           Member member = newMember.get();
       }
   }
   ```
   
   ```java
   public class Member {
       public Member(String name) {}
   }
   
   public class Main {
       public static void main(String[] args) {
           Supplier<Member> newMember = Member::new;
           Member member = newMember.get();
       }
   }
   ```
   
   