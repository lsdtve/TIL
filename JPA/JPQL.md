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

