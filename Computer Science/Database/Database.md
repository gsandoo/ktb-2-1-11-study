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



