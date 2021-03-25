# IoC (Inversion of Control) 

- `제어의 역전`이라고 불린다.
- 예전에는 의존관계의 제어를 개발자가 직접 해주었다.
  그러나 제어권이 컨테이너로 넘어갔고 객체의 생성부터 생명주기의 관리까지 객체에 대한 제어권이 바뀐것을 `IoC`라고 한다.



```java
public class UserService {
  UserRepository userRepository = new UserRepository(); 
}
```

과거에는 위와 같이 개발자가 직접 제어했다.

```java
public class UserService {
  UserRepository userRepository;
  
  @Autowired
  public UserService(UserRepository userRepository){
    this.userRepository = userRepository;
  }
}
```

이것은 개발자가 직접 객체를 관리하지 않고 스프링 컨테이너에서 직접(제어) 객체를 생성하여 해당 객체에 주입 시켜준 것입니다.



이것이 바로 제어가 역전되었다. `IoC` 라는 개념입니다. 



# IoC Contanier

- 스프링 애플리케이션에서는 오브젝트의 생성과 관계설정, 사용, 제거 등의 작업을 애플리케이션 코드 대신 독립된 컨테이너가 담당한다. 이를 컨테이너가 코드 대신 오브젝트에 대한 제어권을 갖고 있다고 해서 IoC라고 부른다. 그래서 스프링 컨테이너를 `IoC 컨테이너`라고도한다.



의존관계 역전 원칙은 두 가지 내용을 담고 있습니다.

1. **상위 모듈은 하위 모듈에 의존해서는 안되고, 인터페이스에 의존해야한다.**
2. **추상화는 세부 상황에 의존해서는 안된다. 세부 사항이 추상화에 의존해야한다**



# 빈 (Bean)

- Spring에서 POJO(plain, old java object)를 `Bean`라고 부른다.
- `Bean`는 애플리케이션의 핵심을 이루는 객체이며, IoC 컨테이너에 의해 인스턴스화, 관리, 생성된다.



### 등록방법

1. **컴포넌트 스캔과 자동 의존관계 설정**

   컴포넌트 스캔의 원리는 기본적으로 `@Component` 어노테이션이 있으면 자동으로 스프링 빈으로 등록된다.

   참고로, `@Component` 어노테이션은` @Controller` , `@Service`, `@Repository`를 포함한다.

2. **자바 코드로 직접 스프링 빈 등록하기**

   `@Configuration` 어노테이션을 추가하고, 스프링 빈으로 등록하고자 하는 Service와 Repository에 `@Bean` 어노테이션을 추가하면, 스프링 빈으로 등록된다.

3. **XML로 스프링 빈 등록하기**

   최근에는 거의 사용하지 않는다.
   
   

Spring-Boot는 어노테이션을 통해 Bean을 설정하고 주입받는 것을 표준으로 삼는다.

```text
- @Bean은 개발자가 컨트롤 할 수 없는 외부 라이브러리 Bean으로 등록하고 싶은 경우 (메소드로 return 되는 객체를 Bean으로 등록) 
- @Component는 개발자가 직접 컨트롤할 수 있는 클래스(직접 만든)를 Bean으로 등록하고 싶은 경우 (선언된 Class를 Bean으로 등록) 
- @Controller, @Service, @Repository 등 은 @Component를 비즈니스 레이어에 따라 명칭을 달리 지정해준 것Container에 있는 Spring Bean을 찾아 주입시켜주는 Annotation
```



### 장점

- 스프링 IoC 컨테이너에 등록된 Bean들은 **의존성 관리**가 수월해진다. 
- 스프링 IoC 컨테이너에 등록된 Bean들은 **싱글톤**의 형태이다



# @Autowired

`@Autowired` 는 각 상황의 타입에 맞는 IoC컨테이너 안에 존재하는 Bean을 자동으로 주입해주게 됩니다.

- required: 기본값은 true (따라서 못 찾으면 애플리케이션 구동 실패)



### 사용할 수 있는 위치

- 생성자 (스프링 4.3 부터는 생략 가능)
- 세터
- 필드