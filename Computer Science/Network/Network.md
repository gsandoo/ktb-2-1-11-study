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

####  프로세스와 스레드 차이를 아시나요?
> 프로세스 : 실행 중인 프로그램의 독립적인 단위. CPU와 메모리 자원을 개별적으로 할당받음

> 스레드 : 프로세스 내 작업의 실행 단위. 동일한 프로세스의 메모리를 공유.

 <br/><br/>

#### 뱅커 알고리즘에 대해 설명 부탁드립니다.
> 뱅커 알고리즘(Banker's Algorithm) : 다중 프로세스 환경에서 교착 상태(Deadlock)를 방지하기 위해 사용하는 자원 할당 알고리즘입니다.


<br/><br/>

#### 브라우저에 www.naver.com을 치면 일어나는 일
> 1. 사용자가 'www.naver.com'을 요청하면, 브라우저와 운영 체제의 로컬 캐시를 먼저 확인한다.

> 2. 캐시에 도메인에 해당하는 정보가 없을 경우, Recursive DNS Server에 DNS Query를 보낸다.

> 3. Recursive DNS Server의 로컬 캐시에서 도메인 네임이 발견되면 매핑된 IP 주소를 반환한다. 그렇지 않은 경우 Root Name Server에 DNS Query를 요청한다.

> 4. Root Name Server는 DNS Query에 따라 올바른 TLD Name Server로 안내한다. 즉, 요청이 www.naver.com 이므로 .com 최상위 도메인을 처리하는 TLD Name Server로 안내한다.

> 5. TLD Name Server는 DNS Query에 따라 올바른 Authoritative Name Server로 안내한다. 즉, 요청이 www.naver.com 이므로 naver.com 2단계 도메인을 처리하는 Authoritative Name Server로 안내한다.

> 6. Authoritative Name Server는 DNS Query에 따라 최종 IP 주소를 반환한다.

> 7. Recursive DNS Server는 전달받은 IP 주소를 클라이언트에 전달하고 로컬 캐시에 저장한다.

> 8. 클라이언트는 전달받은 IP 주소로 'www.naver.com'에 접속한다.

<br/><br/>

#### OSI 7 계층에 대해서 설명해주세요

> 물리 계층 (Physical Layer)은 데이터를 **전기 신호, 광 신호, 전파로 변환**하여 **물리적 매체를 통해 전송**하는 역할을 수행한다.
> - 데이터 전송 단위 : Bit
> - 장비 : 허브, 리피터

> 데이터 링크 계층 (Data Link Layer)은 **MAC 주소를 기반**으로 **같은 LAN에 속한 호스트 간에 데이터를 전송**하는 역할을 수행한다. 
> 이때 프레임(Frame) 단위로 데이터를 처리하고 **오류 검출(CRC)** 과 **기본적인 흐름 제어를 수행**한다.
> - 데이터 전송 단위 : Frame
> - 프로토콜 : Ethernet
> - 장비 : 브릿지, 스위치

> 네트워크 계층 (Network Layer)은 **IP 주소를 기반**으로 데이터를 **다른 네트워크에 속한 호스트에 전달**하는 역할을 수행한다.
> 이때 패킷(Packet) 단위로 데이터를 처리하고 **라우팅 프로토콜**을 통해 목적지까지의 최적 경로를 결정한다.
> - 데이터 전송 단위 : Packet
> - 프로토콜 : IP, ICMP, ARP, OSPF
> - 장치 : 라우터

> 전송 계층 (Transport Layer)은 **포트를 기반**으로 데이터를 **호스트 내의 응용프로그램에 전달**하는 역할을 수행한다.
> 이때 TCP의 경우 세그먼트(Segment) 단위로 데이터를 처리하고 신뢰성있는 통신을 위해 연결 수립, 오류 제어, 흐름 제어, 혼잡 제어를 수행한다.
> UDP의 경우 데이터그램(Datagram) 단위로 데이터를 처리하고 연결 설정 없이 빠르게 통신을 수행한다.
> - 데이터 전송 단위 : Segment(TCP), Datagram(UDP)
> - 프로토콜 : TCP, UDP

> 세션 계층 (Session Layer)은 응용 프로그램 간의 연결 상태를 의미하는 **세션을 설정, 유지, 종료**하는 역할을 수행한다. 이때 데이터 전송 중 **동기화**와 복구를 위한 **체크 포인트**를 설정한다.
> - 프로토콜 : NetBIOS, RPC

> 표현 계층 (Presentation Layer)은 데이터 변환, 압축, 암호화와 같이 **서로 다른 시스템 간 데이터 표현 방식을 표준화**하는 작업을 하는 역할을 수행한다.
> 프로토콜 : SSL/TLS, JPEG

> 응용 계층 (Application Layer)은 사용자와 네트워크 간의 상호작용을 담당하고 **응용 프로그램에게 네트워크 서비스를 제공**하는 역할을 수행한다. 이때 사용자 요청을 적절한 프로토콜로 변환해 하위 계층에 전달한다.
> 프로토콜 : HTTP, FTP, SMTP, DNS, POP3/IMAP

<br/><br/>

#### ARP와 RARP의 차이점을 설명해주세요 

> ARP(Address Resolution Protocol)는 IP 주소를 기반으로 MAC 주소를 알아내기 위한 프로토콜이다. 주로, LAN 내에서 데이터를 주고 받기 위해서 사용한다. 브로드캐스트 요청을 통해 MAC 주소를 확인하며, ARP 테이블에 캐시로 저장한다.

> RARP(Reverse Address Resolution Protocol)는 MAC 주소를 기반으로 IP 주소를 알아내기 위한 프로토콜이다. 주로, IP 주소를 할당 받기 위해서 사용한다.

<br/><br/>

#### L2 스위치와 L3 스위치의 차이점을 설명해주세요

> L2 스위치와 L3 스위치는 네트워크 트래픽을 최적화하기 위해 스위칭 기능을 수행한다.

> L2 스위치는 데이터 링크 계층에서 동작하며, MAC 주소를 기반으로 프레임을 전달한다. LAN 내의 통신에서 주로 사용된다.

> L3 스위치는 네트워크 계층에서 동작하며, IP 주소를 기반으로 패킷을 전달한다. 네트워크 간 통신에서 주로 사용된다.