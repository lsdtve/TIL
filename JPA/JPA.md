# JPA

- Java Persistence API
- 자바 진영의 **ORM** 기술 표준



### ORM이란

- Object-relational mapping(객체 관계 매핑)
- 객체는 객체대로 설계
- 관계형 데이터베이스는 관계형 데이터베이스대로 설계 - ORM 프레임워크가 중간에서 매핑
- 대중적인 언어에는 대부분 ORM 기술이 존재



### JPA는 표준 명세

- JPA는 인터페이스의 모음

- JPA 2.1 표준 명세를 구현한 3가지 구현체

- 하이버네이트, EclipseLink, DataNucleus

![jpa인터페이스](/Users/baeyong-gyun/IdeaProjects/TIL/JPA/JPA.assets/jpa인터페이스-6735131.png)

### JPA 버전

- JPA 1.0(JSR 220) 2006년 : 초기 버전. 복합 키와 연관관계 기능이 부족
- JPA 2.0(JSR 317) 2009년 : 대부분의 ORM 기능을 포함, JPA Criteria 추가
- JPA 2.1(JSR 338) 2013년 : 스토어드 프로시저 접근, 컨버터(Converter), 엔티 티 그래프 기능이 추가



### JPA 동작과정

- JPA는 애플리케이션과 JDBC 사이에서 동작

![jpa-basic-structure](/Users/baeyong-gyun/IdeaProjects/TIL/JPA/JPA.assets/jpa-basic-structure.png)

##### 	저장과정

![jpa-insert-structure](/Users/baeyong-gyun/IdeaProjects/TIL/JPA/JPA.assets/jpa-insert-structure.png)

- MemberDAO에서 객체를 저장할때
  1. JPA에 Entity Object를 넘긴다
  2. JPA는 Entity 분석을하고
  3. INSERT SQL을 생성한다.
  4. JDBC API를 사용하여 SQL을 DB에 날린다.



​	쿼리를 JPA가 만들어 주기 때문에 Object와 RDB 간의 **패러다임 불일치**를 해결할 수 있다.



### JPA을 사용하는 이유

- SQL 중심적인 개발에서 객체 중심으로 개발

- 생산성

  - 간단한 CRUD

    ```java
    저장: jpa.persist(member)
    
    조회: Member member = jpa.find(memberId)
    
    수정: member.setName("변경할 이름")
    
    삭제: jpa.remove(member)
    ```

    

- 유지보수

  - 기존: 필드 변경 시 모든 SQL을 수정해야 한다.

    JPA: 필드만 추가하면 된다. SQL은 JPA가 처리하기 때문에 손댈 것이 없다.

- 패러다임의 불일치 해결

- 성능

- 1. 1차 캐시와 동일성(identity) 보장
  2. 트랜잭션을 지원하는 쓰기 지연(transactional write-behind) 
  3. 지연 로딩(Lazy Loading)

- 데이터 접근 추상화와 벤더 독립성

- 표준

