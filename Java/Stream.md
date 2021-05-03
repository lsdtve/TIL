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



#### 스트림 파이프라인

- 0 또는 다수의 중개 오퍼레이션과 하나의 종료 오퍼레이션으로 구성한다
- 스트림의 데이터 소스는 오직 터미널 오퍼네이션을 실행할 때에만 처리한다



#### 중개 오퍼레이션

- Stream을 리턴한다

- Stateless / Stateful 오퍼레이션으로 더 상세하게 구분할 수도 있다. (대부분은 Stateless지만 distinct나 sorted 처럼 이전 이전 소스 데이터를 참조해야 하는 오퍼레이션은 Stateful 오퍼레이션이다.)

- filter, map, limit, skip, sorted, 등

  

#### 종료 오퍼레이션

- Steam을 리턴하지 않는다
- count, forEach, min, max, collect, allMatch





## 필터링과 슬라이싱

> 스트림의 요소를 선택하는 방법, 스트림의 일부 요소를 무시하거나 크기를 축소하는 방법

- **프레디케이트로 필터링**

  - `filter` 메소드는 프레디케이트 (불린으로 반환하는 함수)를 인수로 받아서 일치하는 모든 요소를 포함하는 스트림을 반환한다.

    ```java
    lst.stream().filter(x>0)
    ```

- **고유 요소 필터링**

  - 고유 요소로 이루어진 스트림을 반환하는 `distinct` (고유 여부는 객체의 hasCode, equals로 결정된다.)
    ```java
    lst.stream().distinct()
    ```

- **스트림 축소**
  
  - 주어진 사이즈 이하의 크기를 갖는 새로운 스트림을 반환하는 `limit(n)`
- **요소 건너뛰기**
  - 처음 n개 요소를 제외한 스트림을 반환하는 `skip(n)`
  - n개 이하의 요소를 포함하는 스트림에 호출하면 빈 스트림이 반환



## 매핑

> 특정 객체에서 특정 데이터를 선택하는 기능

- **스트림의 각 요소에 함수 적용하기**

  - `map` 인수로 제공된 함수는 각 요소에 적용되며 함수를 적용한 결과가 새로운 요소로 매핑된다

    ```java
    List<String> names = member.stream()
      .map(Member::getName)
      .collect(toList());
    ```

    

- **스트림 평면화**

  - `flatMap` 은 하나의 평면화된 스트림을 반환한다.

    ```java
    String[] lst = {"hello", "world"};
    
    List<String> result = Arrays.stream(lst)
      .map(s -> s.split(""))
      .flatMap(Arrays::stream)
      .distinct()
      .collect(Collectors.toList());
    
    // result = {"h", "e", "l", "o", "w", "r", "d"}
    ```

    `map` 을 실행하게 되면 Stream<String[]> 이 생성된다

    여기서 `flatMap`은 스트림의 콘텐츠로 매핑하여 하나의 **평면화된 스트림**을 반환한다.



## 검색과 매칭

> 특정 속성이 데이터 집합에 있는지 여부를 검색하는 데이터 처리
>
> 전체 스트림을 처리하지 않았더라고 결과를 반환하는 쇼트서킷 평가를 사용한다.

- **anyMath**
  - 프리디케이트가 주어진 스트림에서 적어도 한 요소와 일치하는지 확인할 때
- **allMath**
  - 모든 요소가 주어진 프레디케이트와 일치하는지 검사
- **noneMath**
  - allMath와 반대 연산을 수한한다.
  - 프레디케이트와 일치하는 요소가 없는지 확인한다.
- **findAny**
  - 현재 스트림에서 임의의 요소를 반환한다.



## 리듀싱

> 스트림 요소를 조합해서 조금 더 복잡한 질의를 표헌할수 있다.
>
> 모든 스트림 요소를 처리해서 값으로 도출하는 **리듀싱 연산**

- `reduce(초기값, 람다식)`

- **요소의 합**

  ```java
  int sum1 = numbers.stream().reduce(0, (a,b) -> a + b);
  int sum2 = numbers.stream().reduce(0, Integer::sum);
  ```

- **최대값과 최소값**

  ```java
  Optional<Integer> max = numbers.stream().reduce(Integer::max);
  Optional<Integer> min = numbers.stream().reduce(Integer::min);
  ```

  

