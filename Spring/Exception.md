# 예외 (Exception)



### 오류 종류

1. **에러 (Error)**

   - **메모리 부족이나 스택오버플로우** 같이 복구할 수 없는 심각한 오류
   - 개발자가 해결할 수 없는 치명적인 오류

   - 하드웨어의 잘못된 동작 또는 고장으로 인한 오류
   - 에러가 발생되면 프로그램 종류

2. **예외 (Exception)**

   - 개발자가 해결할 수 있는 오류
   - 사용자의 잘못된 조작, 개발자의 잘못된 코딩으로 인한 오류
   - 예외 처리를 하면 정상 실행 상태로 돌아갈 수 있음
   - 예외가 발생하면 비정상적인 종료를 막고, 프로그램을 계속 진행할 수 있도록 우회 경로를 제공하는 것이 바람직



### 예외 종류

1. **일반 예외 (Exception)**

   - 컴파일 시점에서 발생하는 예외

     

2. **실행 예외 (RuntimeException)**

   - 프로그램 실행시에 발생하는 예외



# 예외 처리

>  try/catch 블록은 원래 추하다. 코드 구조에 혼란을 일으키며, 정상 동작과 오류 처리 동작을 뒤섞는다.
>
> 따라, 다음과같은 에러 처리방법이 좋은것같다.

1. **전역 예외 처리 (Global Exception Handling)**

   `@ControllerAdvice`, `@RestControllerAdvice` 으로 모든 예외를 한 곳에서 처리할 수 있다.

   @RestControllerAdvice  = @ControllerAdvice + @ResponseBody

   Web Application 전역적으로 `@ExceptionHandler`를 사용할 수 있다.

   ```java
   @RestControllerAdvice
   public class ExceptionAdvisor {
   
       @ExceptionHandler(BaseException.class)
       public ResponseEntity<ErrorResponseMessage> baseException(BaseException e) {
           ErrorResponseMessage response = new ErrorResponseMessage();
   
           return new ResponseEntity<>(response, HttpStatus.INTERNAL_SERVER_ERROR);
       }
   
   }
   ```

   

2. **Controller 레벨에서 처리**

   `@ExceptionHandler` 어노테이션을 통해 Controller의 메소드에서 throw된 Exception에 대한 공통적인 처리를 할 수 있도록 지원하고 있다.

   ```java
   @Controller
   public class MemberController {
     
       @ExceptionHandler(value=BaseException.class)
       public String hello(BaseException e) {
           return "error";
       }
   }
   ```

   - Controller 메소드 내의 하위 서비스에서 Runtime Exception이 발생하면, 서비스를 호출한 최상위 Controller에서 해당 예외를 처리해준다.

