# 데이터베이스 질문 리스트

간단히 개념들을 정리해보며 머리 속에 넣자~

<br>

### 참고 자료
- [데이터베이스](<https://github.com/kim6394/Dev_BasicKnowledge/blob/master/Interview/Interview List.md#데이터베이스>)

<br>

<br>

### 데이터베이스

---

####  데이터베이스의 Key에 대해서 아시는대로 설명해주세요
>  데이터를 식별하거나 관계를 정의하기 위해 사용

> Primary Key : 테이블에서 각 행을 고유하게 식별 / Not Nullable
 
> Foreign Key : 다른 테이블의 Primary Key를 참조
 
> Candidate Key : Primary Key로 선택할 수 있는 후보 키 / Nullable
 
> Composite Key : 두 개 이상의 컬럼으로 구성된 Primary Key

> Unique Key : 중복 허용 안 되지만 NULL 값은 허용
 
> Super Key : 한 테이블에서 행을 고유하게 식별할 수 있는 모든 키

<br/><br/>

#### 특정 컬럼에 Unique 키워드를 붙혔다고 했을 때, 해당 컬럼을 활용한 쿼리의 성능은 그렇지 않은 컬럼과 비교했을 때 어떻게 다를까요 ?
> Unique 있을 시  : 인덱스가 자동 생성되어 검색, 정렬, 조건문(WHERE, JOIN)의 성능이 향상됩니다.
 
> Unique 없을 시 : 기본적으로 인덱스가 없으므로 전체 테이블 스캔(Full Table Scan)이 발생.

<br/><br/>

#### UNION vs UNION ALL 차이
> 집합 연산자 : 두 개 이상의 SELECT 쿼리 결과를 하나로 결합하여 처리하기 위한 연산자.
 
> 집합 연산자는 UNION, UNION ALL, INTERSECT, EXCEPT로 구성되어 있다.

> UNION : 두 개의 쿼리를 합집합으로 결합한다. 이때 중복된 행은 제거된다.
 
> UNION ALL : 마찬가지로 두 개의 쿼리를 합집합으로 결합하지만 중북된 행도 포함한다.

<br/><br/>

#### ACID 원칙에 대해서 설명해주세요.
> ACID : 트랜잭션이 데이터의 무결성과 일관성을 보장하기 위해 준수해야할 원칙
 
> Atomicity (원자성) : 트랜잭션의 모든 작업이 성공적으로 완료되거나, 하나라도 실패할 경우 모든 작업 취소함
 
> Consistency (일관성) : 트랜잭션 실행 전과 후의 데이터는 데이터베이스의 제약 조건을 준수해야 함

> Isolation (격리성) : 여러 트랜잭션이 동시에 실행되더라도 서로 간섭하지 않고 독립적으로 수행되어야 함

> Durability (지속성) : 트랜잭션이 성공적으로 완료된 후 데이터는 영구적으로 저장되어야 함

<br/><br/>

#### 반정규화에 대해서 설명해 주세요.

> <b>반정규화(Denormalization)</b>는 데이터베이스의 성능 최적화를 위해 정규화된 모델에 중복 데이터를 추가하거나 테이블을 통합하는 작업입니다. 데이터 모델이 비즈니스 로직과 맞지 않아 불필요한 처리가 추가되어야 하는 상황이 발생해서 테이블을 통합했던 경험이 있습니다.

#### 샤딩(Sharding)과 파티셔닝(Partitioning)의 차이에 대해 알려주세요.
> <b>샤딩(Sharding)</b>과 <b>파티셔닝(Partitioning)</b>은 대규모 데이터를 효율적으로 관리하기 위한 데이터베이스 분할 기법입니다.

> <b>샤딩(Sharding)</b>은 데이터베이스를 <span style="color:red;font-weight:bold;">여러 서버에 물리적으로 분산 저장</span>하는 기법으로, 수평 확장(Scale-Out)에 사용합니다.

> <b>파티셔닝(Partitioning)</b>은 <span style="color:red;font-weight:bold;">하나의 데이터베이스 내에서 테이터를 논리적으로 나누는 기법으로 물리적인 서버는 하나</span>입니다. 테이블을 특정 기준에 따라 분리합니다. 실무에서 배치 처리에 시간이 오래 걸려 일자별로 파티셔닝한 경험이 있습니다.

#### Table Full Scan과 Index Range Scan이 어떻게 동작하고 어떤 상황에서 수행되는지 알려주세요.
> <b>Table Full Scan</b>은 테이블의 모든 레코드를 순차적으로 읽으며 필터링 합니다. 적절한 인덱스가 없거나 인덱스를 사용할 수 없는 경우에 수행됩니다.

> <b>Index Range Scan</b>은 인덱스를 사용하여 특정 범위 데이터를 검색합니다. 인덱스 키 값 범위 내에서 탐색하고 해당 레코드만 접근합니다. ``WHERE``절에서 ``BETWEEN``, ``>``, ``<``, ``IN`` 등 범위 연산 사용 시나 테이블 데이터 일부만 읽는 경우 수행됩니다.

#### 데드락에 대해서 설명해 주세요.
> <b>데드락(Deadlock)</b>은 두 개 이상의 트랜잭션이 서로 특정 자원에 대해 잠금 해제를 기다리며 무한 대기 상태에 빠지는 현상입니다. 트랜잭션 타임아웃을 설정하여 대기 시간에 제한을 두에 시간이 초과할 경우 트랜잭션을 강제로 중단하도록 설정한 경험이 있습니다. Spring에서 Anotation Driven 방식으로 Transaction 처리 시 timeout을 초단위로 설정할 수 있습니다.

<br/><br/>
