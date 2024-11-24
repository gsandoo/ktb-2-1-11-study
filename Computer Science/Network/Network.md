# Network 질문 리스트

간단히 개념들을 정리해보며 머리 속에 넣자~

<br>


### 참고 자료 

- [네트워크](<https://github.com/kim6394/Dev_BasicKnowledge/blob/master/Interview/Interview List.md#네트워크>)

<br>

<br>

### Network

---

####  쿠키와 세션의 차이점은? 

 - 💡 질문 의도 : 서버가 유지하려는 데이터가 어떤 위치에 있는지 아는지 의도

> 쿠키 : 클라이언트(브라우저)에 저장. <br/>

> 세션 : 서버에 저장.

<br/><br/>

####  규모가 커져 서버가 여러 개가 된다면, 세션을 어떻게 관리할 수 있을까요? 
- 💡 질문 의도 : 세션 데이터 일관성을 해결할 수 있는 방법을 아는지

> 세션 클러스터링 : 각 서버 간 세션 데이터를 공유하도록 설정

> 세션 스토리지 사용 : Redis나 Memcached 같은 외부 저장소에 세션 데이터 저장
 
> JWT(JSON Web Token) : 세션을 서버가 아닌 클라이언트에서 관리

> Sticky Session : 클라이언트 요청을 항상 같은 서버로 라우팅

<br/><br/>

