# JPQL

- **Java Persistence Query Language**

- 가장 단순한 조회 방법
  - EntityManager.find()
  - 객체 그래프 탐색(a.getB().getC())

- 테이블이 아닌 **객체를 대상으로 검색하는 객체 지향 쿼리**
- SQL을 추상화해서 특정 데이터베이스 SQL에 의존X
- JPA는 SQL을 추상화한 JPQL이라는 객체 지향 쿼리 언어 제공
- SQL과 문법 유사, SELECT, FROM, WHERE, GROUP BY,HAVING, JOIN 지원

- **JPQL은 엔티티 객체를 대상으로 쿼리**를 질의하고

- **SQL은 데이터베이스 테이블을 대상으로 쿼리**를 질의한다.



### 문법

```text
 SELECT :: =
   SELECT_절
   FROM_절
   [WHERE_절]
   [GROUPBY_절]
   [HAVING_절]
   [ORDERBY_절]

 UPDATE :: = UPDATE_절 WHERE_절
 DELETE :: = DELETE_절 WHERE_절 
```

- ```sql
  SELECT m FROM Member AS m WHERE m.username = 'member1'
  ```

- 엔티티 속성은 대소문자를 구분한다. 
- JPQL의 키워드는 대소문자를 구분하지 않는다.
- 별칭은 필수!! (as는 생략 가능)



### 반환타입

#### 1. TypeQuery

```java
TypedQuery<Member> query = em.createQuery("SELECT m FROM Member m", Member.class);
```

- 반환 타입이 명확할 때 사용
- 두번째 파라미터인 클래스로 반환한다.



#### 2. Query

```java
Query query = em.createQuery("SELECT m.username, m.age FROM Member m");
```

- 반환 타입이 명확하지 않을 때 사용
- 조회결과 컬럼이 하나면 Object, 2개 이상일경우 Object[]



### 결과 조회

​	쿼리 객체에서 아래의 메서드들을 사용해 JPQL을 실행한다.

#### query.getResultList()

- **결과가 하나 이상일 때**, 리스트 반환

- 결과가없으면빈리스트반환

#### query.getSingleResult()

- **결과가 정확히 하나**, 단일 객체 반환
- 결과가 없으면 : javax.persistence.NoResultException
- 둘 이상이면 : javax.persistence.NonUniqueResultException



### 파라미터 바인딩

```java
em.createQuery("SELECT m FROM Member m WHERE m.username = :username", Member.class)
    .setParameter("username", "joont1");
```

- 대부분 메서드 체인 방식으로 사용한다.
- 프로퍼티 앞에 : 을 붙여서 바인딩한다.



### 프로젝션

- **SELECT 절에 조회할 대상을 지정하는것**

- 프로젝션 대상

  - 엔티티

    - `SELECT m FROM Member m `
    - `SELECT m.team FROM Member m `

  - 임베디드 타입

    - `SELECT m.address FROM Member m`

  - 스칼라 타입

    - `SELECT m.username, m.age FROM Member m`

    

#### 여러값 조회

```sql
SELECT m.username, m.age FROM Member m
```

1. Query 타입으로 조회

2. Object[] 타입으로 조회

   ```java
   Query query = em.createQuery("SELECT m.username, m.age, m.team FROM Member m");
   List<Object[]> resultList = query.getResultList();
   ```

3. new 명령어로 조회

   ```java
   TypedQuery<UserDTO> query = em.createQuery("
   	SELECT NEW <패키지 명>.UserDTO(m.username, m.age, m.team)
   	FROM Member m",UserDTO.class
   );
   
   List<UserDTO> resultList = query.getResultList();
   ```

   - 순서와 타입이 일치하는 생성자 필요

   - 단순 값을 DTO로 바로 조회
   - 패키지 명을 포함한 전체 클래스 명 입력



### 페이징 API

- **setFirstResult** : 조회 시작 위치
- **setMaxResults** : 조회할 데이터 수

```java
TypedQuery<Member> query = 
    em.createQuery("SELECT m FROM Member m ORDER BY m.username DESC", Member.class);

query.setFirstResult(10);
query.setMaxResult(20);
query.getResultList();
```



### 조인

- 내부 조인

  ```java
  SELECT m FROM Member m [INNER] JOIN m.team t
  ```

- 외부 조인

  ```java
  SELECT m FROM Member m LEFT [OUTER] JOIN m.team t
  ```

- 세타 조인

  ```java
  select count(m) from Member m, Team t where m.username = t.name
  ```

  