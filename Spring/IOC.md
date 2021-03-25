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

3. ~~**XML로 스프링 빈 등록하기**~~

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

```text
singleton : 기본(Default) 싱글톤 스코프. 하나의 Bean 정의에 대해서 Container 내에 단 하나의 객체만 존재한다.
prototype : 어플리케이션에서 요청시 (getBean()) 마다 스프링이 새 인스턴스를 생성
```



# @Autowired

`@Autowired` 는 각 상황의 타입에 맞는 IoC컨테이너 안에 존재하는 Bean을 자동으로 주입해주게 됩니다.

- required: 기본값은 true (따라서 못 찾으면 애플리케이션 구동 실패)



### 사용할 수 있는 위치

- 생성자 (스프링 4.3 부터는 생략 가능)

  ```java
  public class UserService {
    
    UserRepository userRepository;
    
    @Autowired
    public UserService(UserRepository userRepository) {
      this.userRepository = userRepository;
    }
  }
  ```
- 세터

  ```java
  public class UserService {
    
    UserRepository userRepository;
    
    @Autowired
    public setUserService(UserRepository userRepository) {
      this.userRepository = userRepository;
    }
  }
  ```
- 필드

  ```java
  public class UserService {
    
    @Autowired
    UserRepository userRepository;
  }
  ```




### 가능한 경우의 수 

- ~~해당 타입의 빈이 없는 경우~~
- **해당 타입의 빈이 한 개인 경우**
- ~~해당 타입의 빈이 여러 개인 경우~~
  - ~~빈 이름 으로 시도~~,
    - **같은 이름의 빈 찾으면 해당 빈 사용**
    - ~~같은 이름 못 찾으면 실패~~

 

### 같은 타입의 빈이 여러개 일 때

- `@Primary`
- 해당 타입의 빈 모두 주입 받기
- `@Qualifier` (빈 이름으로 주입)



# 빈 스코프

`빈 스코프` 는 빈이 관리되는 범위를 뜻한다.

- `싱글톤`: **기본 스코프**, 스프링 컨테이너의 시작과 종료까지 유지되는 가장 넓은 범위의 스코프이다.

- `프로토타입`: 스프링 컨테이너는 프로토타입 빈의 생성과 의존관계 주입까지만 관여하고 더는 관리하지 않는 매우 짧은 범위의 스코프이다(따라서 빈 콜백중 종료메서드가 호출이 안된다.).

- 웹 관련 스코프
  - `request`: 웹 요청이 들어오고 나갈때 까지 유지되는 스코프이다.
  - `session`: 웹 세션이 생성되고 종료될 때 까지 유지되는 스코프이다.
  - `application`: 웹의 서블릿 컨텍스와 같은 범위로 유지되는 스코프이다.



### 싱글톤 객체 사용시 주의할 점

- 프로퍼티가 공유
- ApplicationContext 초기 구동시 인스턴스 생성.



# Environment 기능

`ApplicationContext`는 `BeanFactory` 기능 말고도 여러가지 기능을 가지고 있다.

`ApplicationContext`는 `EnvironmentCapable`를 상속받고 있다.



EnvironmentCapable은 2가지 기능이 있다.

1. `프로파일`
2. `프로퍼티`



### 프로파일 기능

**Profile이란** 스프링에서 특정 Profile에서만 특정한 빈을 등록하고 싶다거나, 애플리케이션 동작을 특정 Profile에서 설정을 다르게 하고 싶을 때 사용하는 기능이다.

Environmet는 활성화 할 프로파일을 확인하고 설정해주는 것이다.

기본적으로는 default 프로파일로 설정되어있다.



#### 프로파일 정의하기

-  클래스에 정의

   - @Configuration @Profile(“test”)

   -  @Component @Profile(“test”)

-  메소드에 정의

   - @Bean @Profile(“test”)

```java
@Profile("test")
@Configuration
public class TestConfiguration {
    @Bean
    public String test() {
        return "test!";
    }
}
```



#### 프로파일 표현식

- ! (not)

- & (and)
- |(or)



### 프로퍼티 기능

어플리케이션에 등록되어 있는 여러 key-value로 제공되는 프로퍼티에 접근할 수 있는 기능이다.

여러 프로퍼티들은 계층형구조이다.(우선 순위가 존재한다는 뜻)



resources 디렉토리에 `~.properties` 파일을 만들어 사용한다.

```java
my.email = lsdtve@gmail.com
```

다음과 같이 key-value 꼴로 값을 미리정해놓을 수 있다.



```java
@Configuration
@PropertySource("classpath:/app.proerties")
public class TestConfig {
  
}
```

`@PropertySource` 라는 어노테이션을 사용해서 이 어플리케이션이 만들어준 app.properties 파일을 참조할 수 있도록 한다.



##### getProperty

`Environment` 객체의 `getProperty` 메소드를 이용해서 프로퍼티 값을 가져올 수 있다.

.properties 파일의 key에 해당하는 값으로 값을 가져온다.

```java
@Component
public class TestComponent {
  
  @Autowired
  Environment environment;
  
  @PostConstruct
  public void print() {
    System.out.println(environment.getProperty("my.email"));
  }
}
```

