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



