# IOC (Inversion of Control) 

- `제어의 역전`이라고 불린다.
- 예전에는 의존관계의 제어를 개발자가 직접 해주었다.
  그러나 제어권이 컨테이너로 넘어갔고 객체의 생성부터 생명주기의 관리까지 객체에 대한 제어권이 바뀐것을 `IOC`라고 한다.



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

