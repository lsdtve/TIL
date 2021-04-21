# Optional

> **java.util.Optional<T> 클래스**
>
>Optional 객체를 사용하면 예상치 못한 NullPointerException 예외를 제공되는 메소드로 간단히 회피할 수 있습니다.
>
>즉, 복잡한 조건문 없이도 널(null) 값으로 인해 발생하는 예외를 처리할 수 있게 됩니다.



- **Optional<T> 클래스**는 Integer나 Double 클래스처럼 'T'타입의 객체를 포장해 주는 **래퍼 클래스(Wrapper class)**입니다.

  따라서 Optional 인스턴스는 모든 타입의 참조 변수를 저장할 수 있습니다.

  

### 객체의 생성

1. **Optional.empty()**

   비어있는 Optional 객체를 얻어옵니다.

   ```java
   Optional<Member> optMember = Optional.empty();
   ```

2. **Optional.of(value)**

   null이 아닌 객체를 담고 있는 Optional 객체를 생성합니다. null이 들어가면 NPE가 발생합니다.

   ```java
   Optional<Member> optMember = Optional.of(value);
   ```

3. **Optional.ofNullable(value)**

   null인지 아닌지 모르는 객체를 담고있는 Optional객체를 생성합니다

   null이 들어오면 Optional.empty()와 동일하게 동작합니다.

   ```java
   Optional<Member> optMember = Optional.ofNullable(value);
   Optional<Member> optMember = Optional.ofNullable(null);
   ```



### 객체에 접근

1. `get()` : Optional 객체에 저장된 값을 반환함. 저장된 값이 null이면 NPE 발생
2. `isPresent()` :  저장된 값이 존재하면 true를 반환하고, 값이 존재하지 않으면 false를 반환함.
4. `orElse()`  : 저장된 값이 존재하면 그 값을 반환하고, 값이 존재하지 않으면 인수로 전달된 값을 반환함.
5.  `orElseGet()` : 저장된 값이 존재하면 그 값을 반환하고, 값이 존재하지 않으면 인수로 전달된 람다 표현식의 결괏값을 반환함.

3. `orElseThrow()` : 저장된 값이 존재하면 그 값을 반환하고, 값이 존재하지 않으면 인수로 전달된 예외를 발생시킴.

 

### [주의할 것]

- return 값으로만 쓰기를 권장한다.
- Optional을 리턴하는 메소드에서 null을 리턴하지 말자.
  -  (null 인지 모르고 사용할 수 있으므로)

- 프리미티브 타입용 Optional은 따로 있다, ex) `OptionalInt`, `OptionalLong`
