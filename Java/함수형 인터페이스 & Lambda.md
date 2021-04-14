# 함수형 인터페이스 & Lambda



### 함수형 인터페이스

- **추상 메소드**를 딱 하나만 가지고 있는 인터페이스

- **Single Abstract Method** 인터페이스
- `@FuncationInterface` 애노테이션을 가지고 있는 인터페이스



#### 기본 함수형 인터페이스

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