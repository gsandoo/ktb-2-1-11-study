# Spring 질문 리스트

간단히 개념들을 정리해보며 머리 속에 넣자~

<br>

### 참고 자료
- [스프링](<https://github.com/kim6394/Dev_BasicKnowledge/blob/master/Interview/Interview List.md#스프링>)

<br>

<br>

### 스프링

---

####  IoC와 DI 방식에 대해 설명 부탁드립니다.

> IoC(Inversion of Control) : 메소드나 객체의 호출작업을 개발자가 결정하는 것이 아니라, 외부에서 결정되는 것을 의미

> DI : 스프링 컨테이너가 지원하는 핵심 개념 중 하나로, 설정 파일을 통해 객체간의 의존관계를 설정하는 역할을 합니다. <br/>
> 
> 각 클래스 사이에 필요로 하는 의존관계를 Bean 설정 정보 바탕으로 컨테이너가 자동으로 연결합니다.<br/>
> 
> 객체는 직접 의존하고 있는 객체를 생성하거나 검색할 필요가 없으므로 코드 관리가 쉬워지는 장점이 있습니다.

<br/><br/>

#### ORM에서 동적 쿼리 처리를 위해 어떤 기술을 사용하셨나요?

- 💡질문 의도: 동적 쿼리의 의미를 알고, QueryDSL 기술 사용 해봤는지 물어보기 위해

> 동적 쿼리 : 실행 시 조건에 따라 SQL 문을 동적으로 생성하는 쿼리

> QueryDSL : 타입 안전한 Java 기반 ORM(SQL) 빌더로, 코드로 SQL 문을 작성할 수 있게 해주는 도구

<br/><br/>

#### DI를 구현하는 방법 중 생성자 주입, 세터 주입, 필드 주입의 차이점을 설명하고, 가장 권장되는 방법은 무엇인가요?

- 💡질문 의도: 생성자 주입, 세터 주입, 필드 주입의 차이점을 설명 

> 생성자 주입 (Constructor Injection) : 의존성을 생성자의 매개변수로 주입

> 세터 주입 (Setter Injection) : 세터 메서드를 통해 의존성을 주입 <br/>
> 단점 : 객체 생성 후 의존성 누락 가능성.

> 필드 주입 (Field Injection) : @Autowired 등을 사용해 필드에 직접 주입<br/>
> 
> 단점 : <br/>간결하지만 테스트와 유지보수 어려움.<br/>
스프링이 관리하지 않으면 사용 불가.

> 가장 권장되는 방법 <br/>
> - 생성자 주입<br/>
>    - 의존성 누락 방지.<br/>
객체 불변성 보장.<br/>
테스트와 DI 컨테이너 독립성에서 유리.<br/>

<br/><br/>

#### @RestController , @Controller 차이점을 설명해주실 수 있나요?
> @Controller: 뷰를 반환하는 웹 컨트롤러를 정의하는 데 사용됩니다.
 
> @RestController: @Controller와 @ResponseBody를 결합한 편리한 애노테이션입니다.<br> RESTful 웹 서비스를 만들고 응답 본문을 직접 반환하는 데 사용됩니다.

<br/><br/>

#### ORM 환경에서 좋은 엔티티 설계방법이란?
1. 단일 책임 원칙(SRP) 적용
   - 하나의 엔티티는 하나의 테이블 또는 한 가지 개념을 나타내야 한다.
   - 엔티티 클래스에 비즈니스 로직을 너무 많이 포함시키지 말고, 로직은 별도의 서비스 계층에서 처리하도록 한다.

2. 관계 매핑 정확히 설계
   - 엔티티 간 관계를 데이터베이스 모델과 정확히 매핑해야 한다.
- 예시
   ```java
     @OneToMany(mappedBy = "user")
     private List<Order> orders;
   ```
  
  ```java
      @ManyToOne
      @JoinColumn(name = "user_id")
      private User user;
  ```

3. 속성 캡슐화
   - 엔티티 속성은 최대한 캡슐화 하여 접근을 제한한다.
   - 모든 속성을 `private`로 설정한다.
     <br/>
     <br/>
4. DTO를 활용하여 엔티티와 비즈니스 로직을 분리
<br/>
<br/>
5. Lazy Loading을 기본으로 사용

<br/><br/>

#### ORM 인터페이스에서 발생할 수 있는 N+1 문제와 그것을 해결하기 위한 방법
- 💡 `N+1 문제`: 연관 관계가 설정(다대다, 일대다)된 엔티티를 조회할 경우 조회된 데이터 개수 n개 만큼 연관관계의 조회 쿼리가 추가로 발생하는 문제.
- 💡`발생하는 이유`: JPQL이 연관관계를 무시하고 해당 엔티티를 기준으로만 쿼리를 조회하기 때문에 하위 엔티티가 따로 조회가 된다.

>  해결방법: <br/>
> 1. `Fetch Join`을 사용 : but 단점은 페이징 처리 불가
> 2. @EntityGraph에 바로 가져올 필드명을 attributePaths에 지정
> 3. 조회할 때 `distinct` 사용 : ``중복 데이터 제거``
> 4. `BatchSize` 사용 : 여러 개의 프록시 객체를 조회할 때 WHERE 절이 같은 여러 개의 SELECT 쿼리들을 하나의 IN 쿼리로 만듬

<br/><br/>

#### JPA 환경의 동일 트랜잭션에서 반복적인 조회가 발생했을 때, 어떻게 동작하는지
> JPA 1차 캐시와 영속성 컨텍스트 매커니즘에 의해 2차 조회를 하지 않는다.

> 동일한 트랜잭션 내에서 관리되는 엔티티를 영속성 컨텍스트를 통해 1차 캐시에 저장한다. <br/>
> 동일한 엔티티를 반복적으로 조회하면 데이터베이스를 재조회하지 않고, 1차 캐시에서 데이터를 반환한다.

<br/><br/>

#### 선언적 트랜잭션의 동작 방식
> `AOP(Aspect-Oriented Programming)` 를 기반으로 동작 <br/>

> 트랜잭션 어노테이션(@Transactional)을 사용하면 스프링이 해당 메서드를 프록시 객체로 감싸고 <br/>
> 트랜잭션 경계를 자동으로 관리

- 💡기본 동작 과정
> 1. 프록시 생성:
    @Transactional이 붙은 메서드는 프록시 객체로 감싸진다.
    메서드 호출 시, 프록시 객체가 먼저 실행되어 트랜잭션 경계를 설정한다.

> 2. 트랜잭션 시작:
    프록시가 트랜잭션 매니저를 통해 트랜잭션을 시작한다(begin).
    메서드 실행 중 오류가 발생하면 롤백을 수행한다.

> 3. 메서드 실행:
    실제 비즈니스 로직 메서드가 실행된다.
    데이터베이스 작업(읽기, 쓰기 등)은 같은 트랜잭션 범위에서 수행된다.

> 4. 트랜잭션 종료:
    메서드 실행이 성공적으로 완료되면 트랜잭션이 커밋된다.
    예외가 발생하면 트랜잭션이 롤백한다.

<br/><br/>

#### JPA save() 동작방식 - 어떤 상황에서 INSERT가 발생하고 어떤 상황에서 UPDATE가 발생하는지?
> `save()` 메서드 내부에서 주어진 엔티티(객체)가 새로운 엔티티인지, 기존 엔티티인지 판단하여 INSERT 또는 UPDATE SQL을 실행한다.

> 💡 새로운 엔티티(INSERT) 판단 기준 <BR/>
> 엔티티가 영속성 컨텍스트에 관리되지 않는 비영속 상태일 경우 <BR/>
> 엔티티의 식별자(@Id) 값이 null 또는 기본값(예: 0)인 경우 <BR/>

> 💡 기존 엔티티(UPDATE) 판단 기준 <BR/>
> 엔티티의 식별자(@Id) 값이 이미 설정되어 있는 경우. <BR/>
> 영속성 컨텍스트에 해당 엔티티가 존재하거나, 데이터베이스에서 조회 가능한 경우. <BR/>

> 💡 save 메서드 내부동작 흐름 <BR/>
> 엔티티의 식별자 값을 확인하여 새로운 엔티티인지 판단. <BR/>
> > 새로운 엔티티라면 `EntityManager.persist()` 호출. <BR/>
> > 기존 엔티티라면 `EntityManager.merge()` 호출. <BR/>

<br/><br/>

#### Spring Bean과 등록 방법에 대해서 설명해주세요
> 1. XML 파일을 사용한 Bean 등록 <br/>

> >  초기 스프링 프레임워크에서 사용되던 방식
```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="myBean" class="com.example.MyBean" />
</beans>
```

> 2.  Java Config(@Configuration) 방식

>> Java 기반의 설정 클래스를 사용하여 Bean을 등록하는 방식.

```java
@Configuration
public class AppConfig {

    @Bean
    public MyBean myBean() {
        return new MyBean();
    }
}
```

> 3. Annotation 기반 방식

>> 클래스에 직접 어노테이션을 추가하여 Bean을 등록

> `@Component`: 일반적인 Spring Bean 등록. <br/>
> `@Service`: 서비스 레이어에서 사용되는 Bean에 주로 사용.<br/>
> `@Repository`: DAO(Data Access Object) 레이어에서 사용.<br/>
> `@Controller`: Spring MVC에서 컨트롤러로 사용.
> 
```java
@Component
public class MyBean {
    // Bean 클래스 정의
}

```
<br/><br/>

#### Spring Bean의 Scope 개념에 대해 설명해주세요.
> Spring Bean의 Scope는 Spring IoC 컨테이너가 Bean의 생성 방식과 생명주기를 관리하는 방식을 정의합니다<br/>
> Scope는 Bean의 인스턴스가 생성되고 사용되는 범위를 결정하는 설정

> Spring의 주요 Bean scope

> 1. Singleton (기본 스코프)
>> Spring 컨테이너당 하나의 Bean 인스턴스를 생성하고 관리<br/>
>> 모든 요청이 동일한 인스턴스를 공유.
> 2. Prototype
>> Bean 요청 시마다 새로운 인스턴스를 생성
> 3. Request (웹 애플리케이션 전용)
>> HTTP 요청당 하나의 Bean 인스턴스를 생성

