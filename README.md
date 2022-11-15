# HTTP-web-network

#소개영상
-모든것이 HTTP 기반 위에서 동작한다.
-처음 웹개발을 공부하는 개발자
-실무에서 웹 기술을 사용하는 개발자

#1 인터넷 네트워크
#인터넷 통신
-메시지가 전송되는것을 이해하기 위해서는 IP(인터넷 프로토콜)에 대해서 알아야함.

#IP(인터넷 프로토콜)
-복잡한 인터넷 망에서 최소한의 규칙 -> IP 주소를 부여함으로써 가능.
-IP 인터넷 프로토콜 역할
 지정한 주소(IP Address)에 데이터 전달
 패킷(Packet)이라는 통신 단위로 데이터 전달
-IP 패킷 정보(출발지 IP, 목적지 IP, 기타...) -> 클라이언트 패킷 전달 -> 서버 패킷 전달
*IP 프로토콜의 한계
(1)비연결성 -> 패킷을 받을 대상이 없거나 서비스 불능 상태여도 패킷 전송
(2)비신뢰성 -> 중간에 패킷이 사라지면?, 패킷이 순서대로 안오면?
(3)프로그램 구분 -> 같은 IP를 사용하는 서버에서 통신하는 애플리케이션이 둘 이상이라면?
-대상이 서비스 불능, 패킷 전송 -> 대상 서버가 패킷을 받을 수 있는 상태인지 모름
-패킷 소실 -> 중간에 패킷이 소실되면 방법이 없음(소실되도 모름).
-패킷 전달 순서 문제 발생 -> 한번에 보내는 용량이 너무 많으면 나눠서 보내는데 서로 다른 노드를 탈수 있음. 그래서 순서가 바뀔 수 있음. 
-IP 프로토콜 만으로는 이런 문제들을 해결하 수 없음.

#TCP, UDP
*인터넷 프로토콜 스택의 4계층
-애플리케이션 계층 - HTTP, FTP
-전송 계층 - TCP, UDP
-인터넷 계층 - IP
-네트워크 인터페이스 계층

*프로토콜 계층
-애플리케이션 (웹브라우저 네트워크 게임 채팅 프로그램
                        SOCKET 라이브러리            )
-OS (TCP
     IP(Internet Protocol))                    
-네트워크 인터페이스 ( LAN 드라이버
                       LAN 장비   )      
1. 프로그램이 Hello, world! 메시지 생성
2, SOCKET 라이브러리를 통해 전달
3. TCP 정보 생성, 메시지 데이터 포함
2. IP 패킷 생성, TCP 데이터 포함        

-TCP/IP 패킷 정보 - (출발지 IP, 목적지 IP, 기타...(출발지 PORT, 목적지 PORT, 전송 제어, 순서, 검증 정보...(전송 데이터)))
-패킷이란? -> 패키지(package) + 덩어리(bucket)

*TCP 특징 (전송제어 프로토콜(Transmission Control Protocol))
-연결지향 TCP 3 way handshake (가상 연결)
-데이터 전달 보증
-순서 보장
-신뢰할 수 있는 프로토콜
-현재는 대부분 TCP 사용

*TCP 3 way handshake
1.SYN
2.SYN+ACK
3.ACK (요즘은 3번에서 데이터 전송)
4.데이터 전송
-논리적으로만 연결이됀것. 중간에 수많은 서버(노드)를 거치지않음. 나를 위한 전용 랜선이 보장 X

*데이터 전달 보증
1. 데이터 전송
2. 데이터 잘받았음

*순서 보장
1. 클라이언트 -> 패킷1, 패킷2, 패킷3 순서로 전송 -> 서버
2. 패킷1, 패킷3, 패킷2 순서로 도착 -> 서버
3. 서버 -> 패킷2부터 다시 보내! -> 클라이언트

*UDP 특징 (사용자 데이터 프로그램(User Datagram Protocol))
-하얀 도화지에 비유(기능이 거의 없음)
-연결지향 TCP 3 way handshake X
-데이터 전달 보증 X 
-순서 보장 X 
-데이터 전달 및 순서가 보장되지 않지만, 단순하고 빠름
-정리
1. IP와 거의 같다. +PORT +체크섬 정도만 추가
2. 애플리케이션에서 추가 작업 필요

#PORT
-PORT 뜻 : 항구
-한번에 둘 이상 연결해야 하면? -> TCP/IP 패킷 (출발지 IP & PORT, 목적지 IP & PORT, 전송 데이터...)
-PORT -> 같은 IP 내에서 프로세스 구분
-이해하기 쉽게 : IP (아파트) PORT (몇동 몇호)
*PORT
- 0 ~ 65535 할당 가능
- 0 ~ 1023 : 잘 알려진 포트, 사용하지 않는 것이 좋음
  FTP - 20, 21
  TELNET - 23
  HTTP - 80
  HTTPS - 443

#DNS
-IP는 기억하기 어렵다. IP는 변경될 수 있다. -> DNS를 사용함으로써 해결됨.
*DNS (도메인 네임 시스템(Domain Name System))
- 전화번호부 같은 서버 제공
- 도메인 명을 IP 주소로 변환

-DNS 사용
1. 도메인 명 google.com
2. 응답 200.200.200.2
2. 서버 200.200.200.2
        DNS 서버
 도메인 명         IP
google.com    200.200.200.2
aaa.com       210.210.210.3

#인터넷 네트워크 정리
-인터넷 통신
-IP(Internet Protocol) -> 메시지를 보내기 위해서 필요함. IP 프로토콜만 가지고는 메시지가 잘도착했는지 신뢰하기 어렵고, PORT 기능도 X
-TCP, UDP -> TCP: IP 프로토콜의 문제점을 해결해줌. UDP: IP와 거의 똑같은데 PORT 정도만 추가됨. 필요하면 기능 확장 가능
-PORT -> 같은 IP 안에서 통신하는 애플리케이션을 구분하기 위해 사용
-DNS -> IP는 변하기 쉽고, 외우기 어려움. 도메인 명을 등록해서 사용할 수 있도록 도와줌.


#2 URI와 웹 브라우저 흐름
#URI
-URI(Uniform Resource Identifier)
*URI? URL? URN? 
-URI는 로케이터(locator), 이름(name) 또는 둘 다 추가로 분류될 수 있다.
-            URI(Resource Identifier)
( (URL: Resource Locator)  (URN: Resource Name) )

*URI 단어뜻
-Uniform: 리소스 식별하는 통일된 방식
-Resource: 자원, URI로 식별할 수 있는 모든 것(제한 없음)
-Identifier: 다른 항목과 구분하는데 필요한 정보

-URL: Uniform Resource Locator
-URN: Uniform Resource Name
#웹 브라우저 요청 흐름

*URL, URN 단어 뜻
-URL -> Locator: 리소스가 있는 위치를 지정
-URN -> Name: 리소스에 이름을 부여
-위치는 변할 수 있지만, 이름은 변하지 않는다.
-urn:isbm:8960777331 (어떤 책의 isbn URN)
-URN 이름만으로 실제 리소스를 찾을 수 있는 방법이 보편화 되지 않음.
-앞으로 URI를 URL과 같은 의미로 이야기하겠음.

*URL 전체 문법
- scheme://[userinfo@]host[:port][/path][?query][#fragment]
- https://www.goole.com:443/search?q=hello&hl=ko

- 프로토콜(https)
- 호스트명(www.google.com)
- 포트 번호(443)
- 패스(/search)
- 쿼리 파라미터(q=hello&hl=ko)

*URL scheme
-scheme
-https
- 주로 포로토콜 사용
- 프로토콜: 어떤 방식으로 자원에 접근할 것인가 하는 약속 규칙
   예) http, https, ftp 등등
- http는 80 포트, https는 443 포트를 주로 사용, 포트는 생략 가능
- https는 http에 보안 추가 (HTTP Secure)

*URL userinfo
-[userinfo@]
-URL에 사용자 정보를 포함해서 인증
-거의 사용하지 않음

*URL host
-host
-www.google.com
-호스트명
-도메인명 또는 IP 주소를 직접 사용가능

*URL PORT
-[:port]
-443
-포트(PORT)
-접속 포트
-일반적으로 생략, 생략시 http는 80, https는 443

*URL path
-[/path]
-/search
-리소스 경로(path), 계층적 구조
-예)
  - /home/file1.jpg
  - /members
  - /members/100, /items/iphone12

*URL query
-[?query]
-?q=hello&hl=ko
-key=value 형태
-?로 시작, &로 추가 가능 ?keyA=valueA&keyB=valueB
-query parameter, query string 등으로 불림, 웹서버에 제공하는 파라미터. 문자 형태

*URL fragment
-[#fragment]
-#getting-started-introducing-spring-boot
-fragment
-html 내부 북마크 등에 사용
-서버에 전송하는 정보 아님

#웹브라우저 요청 흐름
-HTTP 요청 메시지 : GET /search?q=hello&hl=ko HTTP/1.1
                    HOST: www.google.com 
-HTTP 메시지 전송
1.웹브라우저가 HTTP 메시지 생성
2. SOCKET 라이브러리를 통해 전달
     -A: TCP/IP 연결(IP, PORT)
     -B: 데이터 전달
3.TCP/IP 패킷 생성, HTTP 메시지 포함
-HTTP 응답 메시지 : HTTP/1.1 200 OK
                    Content-Type: text/html;charset=UTF-8
                    Content-Length: 3423
                    <html>
                      <body>...</body> 
                    </html> 
*[HTTP]
-모든 것이 HTTP
-클라이언트 서버 구조
-Stateful, Stateless
-비 연결성(connectionless)
-HTTP 메시지

#3 HTTP 기본
#모든 것이 HTTP
-HTTP : Hyper Text Transfer Protocol

*모든 것이 HTTP (HTTP 메시지에 모든 것을 전송)
-HTML, TEXT
-IMAGE, 음성, 영상, 파일
-JSON, XML (API)
-거의 모든 형태의 데이터 전송 가능
-서버간에 데이터를 주고 받을 때도 대부분 HTTP 사용
-지금은 HTTP 시대!

* HTTP 역사
-HTTP/0.9 1991년: GET 메서드만 지원, HTTP 헤더X
-HTTP/1.0 1996년: 메서드, 헤더 추가
-HTTP/1.1 1997년: 가장 많이 사용, 우리에게 가장 중요한 버전
 - RFC2068 (1997) -> RFC2616 (1999) -> RFC7230~7235 (2014)
-HTTP/2 2015년: 성능개선
-HTTP/3 진행중: TCP 대신에 UDP 사용, 성능 개선

*기반 프로토콜
-TCP: HTTP/1.1, HTTP/2
-UDP: HTTP/3
-현재 HTTP/1.1 주로 사용
 -HTTP/2, HTTP/3도 점점 증가

*HTTP 특징
-클라이언트 서버 구조
-무상태 프로토콜(스테이트리스), 비연결성
-HTTP 메시지
-단순함, 확장 가능

#클라이언트 서버 구조
-Request Response 구조
-클라이언트는 서버에 요청을 보내고, 응답을 대기
-서버가 요청에 대한 결과를 만들어서 응답
-클라이언트와 서버를 분리하는 것이 중요 -> 서버: 비즈니스 로직, 데이터 / 클라이언트 : ui/ux에 집중
-양쪽이 독립적으로 진화를 할 수 있다는 것이 중요

#무상태 프로토콜 - 스테이트리스(Stateless)
-서버가 클라이언트의 상태를 보존X
-장점: 서버 확장성 높음(스케일 아웃)
-단점: 클라이언트가 추가 데이터 전송

*Stateful, Stateless 차이
*상태 유지(Stateful) : 중간에 다른 점원으로 바뀌면 안된다.
(중간에 다른 점원으로 바뀔 때 상태 정보를 다른 점원에게 미리 알려줘야 한다.)
*무상태(Stateless) : 중간에 다른 점원으로 바뀌어도 된다.
 -갑자기 고객이 증가해도 점원을 대거 투입할 수 있다.
 -갑자기 클라이언트 요청이 증가해도 서버를 대거 투입할 수 있다.
: 무상태는 응답 서버를 쉽게 바꿀 수 있다. -> 무한한 서버 증설 가능

*상태 유지(Stateful) 특징
-항상 같은 서버가 유지되어야한다.
1.요청 : 클라이언트A -> 2.응답 : 서버 ('상태 유지' 클라이언트A: 노트북 ,2개)

*무상태(Stateless) 특징
-아무 서버나 호출해도 된다.
1.요청 : 클라이언트A (노트북, 2개 포함) -> 2.응답 : 서버 (상태를 보관하지 않는다.)
-중간에 서버가 장애나면? -> 서버2로 전달
-스케일 아웃 -> 수평 확장 유리 
 예) 큰 이벤트를 하면 장비를 수십대, 수백대로 늘릴 수 있다.

*무상태(Stateless) 실무 한계
-모든 것을 무상태로 설계 할 수 있는 경우도 있고 없는 경우도 있다.
-무상태
 -예) 로그인이 필요 없는 단순한 서비스 소개 화면
-상태 유지
 - 예) 로그인
-로그인한 사용자의 경우 로그인 했다는 상태를 서버에 유지
-일반적으로 브라우저 쿠키와 서버 세션등을 사용해서 상태 유지
-상태 유지는 최소한만 사용


#비연결성(connectionless)
*연결을 유지하는 모델
-클라이언트가 놀고있어도 서버는 연결을 계속 유지해야하는 단점이 있다. 서버의 자원이 소모됨.

*연결을 유지하지 않는 모델
-1. 클라이언트 요청 -> 2. 서버 응답 -> 3. TCP/IP 연결 종료 
-서버는 연결 유지X, 최소한의 자원 유지

*비연결성
-HTTP는 기본이 연결을 유지하지 않는 모델
-일반적으로 초 단위의 이하의 빠른 속도로 응답
-1시간 동안 수천명이 서비스를 사용해도 실제 서버에서 동시에 처리하는 요청은 수십개 이하로 매우 작음
 -예) 웹 브라우저에서 계속 연속해서 검색 버튼을 누르지는 않는다.
-서버 자원을 매우 효율적으로 사용할 수 있음

*비연결성 : 한계와 극복
-TCP/IP 연결을 새로 맺어야함 - 3 way handshake 시간 추가
-웹 브라우저로 사이트를 요청하면 HTML 뿐만 아니라 자바스크립트, css, 추가 이미지 등등 수 많은 자원이 함께 다운로드
-지금은 HTTP 지속 연결(Persistent Connections)로 문제 해결
-HTTP/2, HTTP/3에서 더 많은 최적화

*HTTP초기 - 연결, 종료 낭비
-클라이언트   -연결 0.1초                    - 서버 
              -요청/HTML 응답 0.1초 -
              -종료 0.1초 -

              -연결 0.1초 -
              -요청/자바스크립트 응답 0.1초 -
              -종료 0.1초 -

              -연결 0.1초 -
              -요청/이미지 응답 0.1초 -
              -종료 0.1초 -
-합 : 0.9초

*HTTP 지속 연결(Persistent Connections)
-클라이언트 -      -연결 0.1초                    -서버
                   -요청/HTML 응답 0.1초 -
                   -요청/자바스크립트 응답 0.1초 -
                   -요청/이미지 응답 0.1초 -
                   -종료 0.1초 -
-합 : 0.5초

*스테이트리스를 기억하자
서버 개발자들이 어려워하는 업무
-정말 같은 시간에 딱 맞추어 발생하는 대용량 트래픽
 -예) 선착순 이벤트, 명절 KTX 예약, 학과 수업 등록
 -예) 저녁 6:00 선착순 1000명 치킨 할린 이벤트 -> 수만명 동시 요청

#HTTP 메시지
*모든 것이 HTTP - 한번 더!
HTTP 메시지에 모든 것을 전송
-HTML, TEXT
-IMAGE, 음성, 영상, 파일
-거의 모든 형태의 데이터 전송 가능
-서버간에 데이터를 주고 받을 때도 대부분 HTTP 사용
-지금은 HTTP 시대!

-HTTP 메시지 구조
start-line 시작 라인
header 헤더
empty line 공백 라인 (CRLF)
message body

-예) HTTP 요청 메시지
GET /search?q=hello&hl=ko HTTP/1.1
Host: www.google.com
공백 line
-요청 메시지도 body 본문을 가질 수 있음

-예) HTTP 응답 메시지
HTTP/1.1 200 OK
Content-Type: text/html;charset-UTF-8
Content-Length: 3423
공백 line
<html>
 <body>...</body>
</html> 

-공식 스펙
start-line
* ( header-field CRLF)
CRLF
[ message-body ]

*시작 라인
요청 메시지
-start-line = request-line / status-line
-request-line = mothod SP(공백) request-target SP HTTP-version CRLF(엔터)

-HTTP 메서드 (GET: 조회)
-요청 대상 (/search?q=hello&hl=ko)
-HTTP Version

*시작 라인
요청 메시지 - HTTP 메서드
-종류: GET, POST, PUT, DELETE...
-서버가 수행해야 할 동작 지정
 -GET: 리소스 조회
 -POST: 요청 내역 정리

*시작 라인
요청 메시지 - 요청 대상
-absoulte-path[?query] (절대경로[?쿼리])
-절대 경로="/"로 시작하는 경로
-참고: *, http://...?x=y 와 같이 다른 유형의 경로지정 방법도 있다.

*시작 라인
요청 메시지 - HTTP 버전
-HTTP 버전

*시작 라인 
응답 메시지
-start-line = request-line / status-line
-status-line = HTTP-version SP status-code SP reason-phrase CRLF

-HTTP 버전
-HTTP 상태 코드: 요청 성공, 실패를 나타냄
 -200: 성공
 -400: 클라이언트 요청 오류
 -500: 서버 내부 오류
-이유 문구: 사람이 이해할 수 있는 짧은 상태 코드 설명 글

*HTTP 헤더
-header-field = field-name ":" OWS filed-value OWS (OWS:띄어쓰기 허용)
-field-name은 대소문자 구분 없음

*HTTP 헤더
용도
-HTTP 전송에 필요한 모든 부가정보
 -예) 메시지 바디의 내용, 메시지 바디의 크기, 압축, 인증, 요청 클라이언드(브라우저)정보,
 서버 애플리케이션 정보, 캐시 관리 정보...
-표준 헤더가 너무 많음 https://en/WiKipedia.org/WiKi/List of HTTP header fields
-필요시 임의의 헤더 추가 가능
 -helloworld: hihi

*HTTP 메시지 바디
용도
-실제 전송할 데이터
-HTML 문서, 이미지, 영상, JSON 등등 byte로 표현할 수 있는 모든 데이터 전송 가능

*단순함 & 확장 가능
-HTTP는 단순하다. 스펙도 읽어볼만...
-HTTP 메시지도 매우 단순
-크게 성공하는 표준 기술은 단순하지만 확장 가능한 기술

*HTTP 정리
-HTTP 메시지에 모든 것을 전송
-HTTP 역사 HTTP/1.1을 기준으로 학습
-클라이언트 서버 구조
-무상태 프로토콜(스테이트리스)
-HTTP 메시지
-단순함, 확장 가능
-지금은 HTTP 시대

#4. HTTP 메서드
#HTTP API를 만들어보자
*요구 사항
회원 정보 관리 API를 만들어라.
-회원 목록 조회
-회원 조회
-회원 등록
-회원 수정
-회원 삭제

*API URI 설계 
URI(Uniform Resource Identifier)
-회원 목록 조회 /read-member-list
-회원 조회 /read-member-by-id
-회원 등록 /create-member
-회원 수정 /update-member
-회원 삭제 /delete-member
-이것은 좋은 URI 설계일까?
*가장 중요한 것은 리소스 식별

*API URI 고민
URI(Uniform Resource Identifier)
-리소스의 의미는 뭘까?
 -회원을 등록하고 수정하고 조회하는게 리소스가 아니다!
 -예) 미네랄을 캐라 -> 미네랄이 리소스
 -회원이라는 개념 자체가 바로 리소스다. (중요)
-리소스를 어떻게 식별하는게 좋을까?
 -회원을 등록하고 수정하고 조회하는 것을 모두 배제
-회원이라는 리소스만 식별하면 된다. -> 회원 리소스를 URI에 매핑

*API URI 설계 
URI(Uniform Resource Identifier)
-"회원" 목록 조회
-"회원" 조회 
-"회원" 등록 
-"회원" 수정
-"회원" 삭제 

*API URI 설계
리소스 식별, URI 계층 구조 활용
-회원 목록 조회 /members
-회원 조회 /members/{id} -> 어떻게 구분하지?
-회원 등록 /members/{id} -> 어떻게 구분하지?
-회원 수정 /members/{id} -> 어떻게 구분하지?
-회원 삭제 /members/{id} -> 어떻게 구분하지? 
-참고: 계층 구조상 상위를 컬렉션으로 보고 복수단어 사용 권장(member -> members)

*리소스와 행위를 분리
가장 중요한 것은 리소스를 식별하는 것
-URI는 리소스만 식별! (중요)
-리소스와 해당 리소스를 대상으로 하는 행위를 분리
 -리소스: 회원
 -행위: 조회, 등록, 삭제, 변경
-리소스는 명사, 행위는 동사 (미네랄을 캐라)
-행위(메서드)는 어떻게 구분?

#HTTP 메서드 - GET, POST
-HTTP 메서드: 클라이언트가 서버에 뭔가를 요청할 때 기대하는 행동

*HTTP 메서드 종류
주요 메서드
-GET: 리소스 조회
-POST: 요청 데이터 처리, 주로 등록에 사용
-PUT: 리소스를 대체, 해당 리소스가 없으면 생성
-PATCH: 리소스 부분 변경
-DELETE: 리소스 삭제

*HTTP 메서드 종류
기타 메서드
-HEAD: GET과 동일하지만 메시지 부분을 제외하고, 상태 줄과 헤더만 반환
-OPTIONS: 대상 리소스에 대한 통신 가능 옵션(메서드)을 설명(주로 CORS에서 사용)
-CONNECT: 대상 자원으로 식별되는 서버에 대한 터널을 설정
-TRACE: 대상 리소스에 대한 경로를 따라 메시지 루프백 테스트를 수행

*GET
-리소스 조회
-서버에 전달하고 싶은 데이터는 query(쿼리 파라미터, 쿼리 스트링)를 통해서 전달
-메시지 바디를 사용해서 데이터를 전달할 수 있지만, 지원하는 곳이 많지 않아서 권장하지 않음.

*리소스 조회1 - 메시지 전달
: 클라이언트 -> GET -> 서버
*리소스 조회2 - 서버도착
: 클라이언트 -> GET 서버
*리소스 조회3 - 응답 데이터
: 클라이언트 <- Response <- 서버

*POST
-요청 데이터 처리
-'메시지 바디를 통해 서버로 요청 데이터 전달'
-서버는 요청 데이터 '처리'
 -메시지 바디를 통해 들어온 데이터를 처리하는 모든 기능을 수행한다.
-주로 전달된 데이터로 신규 리소스 등록, 프로세스 처리에 사용

*리소스 등록1 - 메시지 전달 
: 클라이언트 -> POST -> 서버
*리소스 등록2 - 신규 리소스 생성
: 서버 - 신규 리소스 식별자 생성
*리소스 등록2 - 응답 데이터
: 클라이언트 <- Response <- 서버

*POST
요청 데이터를 어떻게 처리한다는 뜻일까? 예시
-스펙: POST 메서드는 대상 리소스가 고유한 의미 체계에 따라 요청에 포함된 표현을 처리하도록 요청합니다.
-예를들어 POST는 다음과 같은 기능에 사용됩니다.
 -HTML 양식에 입력된 필드와 같은 데이터 블록을 데이터 처리 프로세스에 제공
  -예) HTML FORM에 입력한 정보로 회원가입, 주문 등에서 사용
 -게시판, 뉴스 그룹, 메일링 리스트, 블로그 또는 유사한 기사 그룹에 메시지 게시
  -예) 게시판 글쓰기, 댓글 달기 
 -서버가 아직 식별하지 않은 새 리소스 생성
  -예) 신규 주문 생성
 -기존 자원에 데이터 추가
  -예) 한 문서 끝에 내용 추가하기
 -정리: 이 리소스 URI에 POST 요청이 오면 데이터를 어떻게 처리할지 리소스마다 따로 정해야 함 -> 정해진 것이 없다.

*POST 
정리
1.새 리소스 생성 (등록)
-서버가 아직 식별하지 않은 새 리소스 생성
2.요청 데이터 처리 (중요)
-단순히 데이터를 생성하거나, 변경하는 것을 넘어서 프로세스를 처리해야 하는 경우
 -예) 주문에서 결제완료 -> 배달 시작 -> 배달완료 처럼 단순히 값 변경을 넘어 프로세스의 상태가 변경되는 경우
-POST의 결과로 새로운 리소스가 생성되지 않을 수도 있음
 -예) POST /orders/{orderd}/start-delivery (컨트롤 URI)
3.다른 메서드로 처리하기 애매한 경우
 -예) JSON으로 조회 데이터를 넘겨야 하는데, GET 메서드를 사용하기 어려운 경우
-애매하면 POST       

#HTTP 메서드 - PUT, PATCH, DELETE
*PUT                                        
-리소스를 대체 
 -리소스가 있으면 대체
 -리소스가 없으면 생성
 -쉽게 이야기해서 덮어버림
-중요! 클라이언트가 리소스를 식별 
 -클라이언트가 리소스 위치를 알고 URI 지정 (PUT /menbers/100 HTTP/1.1)
 -POST와 차이점 

*PUT 
*리소스가 있는 경우1
-클라이언트 -> PUT /members/100 {
  "username": "old",
  "age": 50
}  -> 서버 {
  "username": "young",
  "age": 20
}
리소스가 있는 경우2
-리소스 대체 
-> 서버 {
  "username": "old",
  "age": 50
}
*리소스가 없는 경우 -> 신규 리소스 생성
*주의! 리소스를 완전히 대체한다1
-클라이언트                     ->   PUT   ->      서버 
PUT /members/100 HTTP/1.1                       {
                                                  "username": "young",
                                                  "age": 20
                                                            }
Content-Type: application/json
{
  "age": 50
}
:username 필드 없음

*주의! 리소스를 완전히 대체한다2
-서버 
{
  "age": 50
}
:username 필드 삭제됨

*PATCH
-리소스 부분 변경

*DELETE
-리소스 제거


#HTTP 메서드의 속성
*안전
Safe
-호출해도 리소스를 변경하지 않는다.
-Q: 그래도 계속 호출해서, 로그 같은게 쌓여서 장애가 발생하면요?
-A: 안전은 해당 리소스만 고려한다. 그런 부분까지 고려하지않는다.

*멱등
Indempotent
-f(f(x)) = f(x)
-한번 호출하든 두번 호출하든 100 호출하든 결과가 똑같다.
-멱등 메서드
 -GET: 한번 조회하든, 두번 조회하든 같은 결과가 조회된다.
 -PUT: 결과를 대체한다. 따라서 같은 요청을 여러번 해도 최종 결과는 똑같다.
 -DELETE: 결과를 삭제한다. 같은 요청을 여러번 해도 삭제된 결과는 똑같다.
 -POST: 멱등이 아니다! 두번 호출하면 같은 결제가 중복해서 발생할 수 있다.

*멱등
Indempotent
-활용
 -자동 복구 메커니즘
 -서버가 TIMEOUT 등으로 정상 응답을 못주었을 때, 클라이어트가 같은 요청을 다시 해도 되는가? 판단 근거

*멱등
Indempotent
-Q: 재요청 시간에 중간에 다른 곳에서 리소스를 변경해버리면?
 -사용자1: GET -> username:A, age:20
 -사용자2: PUT -> username:A, age:30
 -사용자1: GET -> username:A, age:30 -> 사용자2의 영향으로 바뀐 데이터 조회
-A: 멱등은 외부 요인으로 중간에 리소스가 변경되는 것까지는 고려하지는 않는다.

*캐시가능
Cacheable
-응답 결과 리소스를 캐시해서 사용해도 되는가?
-GET, HEAD, POST, PACTH 캐시가능
-실제로는 GET, HEAD 정도만 캐시로 사용
 -POST, PACTH는 본문 내용까지 캐시 키로 고려해야 하는데, 구현이 쉽지 않음

