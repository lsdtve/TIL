# Stream

> sequence of elements supporting sequential and parallel aggregate operations

- Java8 에서 추가되었고 람다를 활용할 수 있는 기술이다.

- `데이터의 흐름` 이다

- 데이터를 담고 있는 저장소가 아니다

- 스트림이 처리하는 데이터 소스를 변경하지 않는다

- 손쉽게 병렬 처리할 수 있다

  ```text
  스트림 인스턴스 생성 -> 중개 오퍼레이션(0개 또는 다수) -> 종료 오퍼레이션
  ```

  이렇게 크게 세 가지로 나눌 수 있다.



### 스트림 파이프라인

- 0 또는 다수의 중개 오퍼레이션과 하나의 종료 오퍼레이션으로 구성한다
- 스트림의 데이터 소스는 오직 터미널 오퍼네이션을 실행할 때에만 처리한다



### 중개 오퍼레이션

- Stream을 리턴한다
- Stateless / Stateful 오퍼레이션으로 더 상세하게 구분할 수도 있다. (대부분은 Stateless지만 distinct나 sorted 처럼 이전 이전 소스 데이터를 참조해야 하는 오퍼레이션은 Stateful 오퍼레이션이다.)
- filter, map, limit, skip, sorted, 등



### 종료 오퍼레이션

- Steam을 리턴하지 않는다
- count, forEach, min, max, collect, allMatch

