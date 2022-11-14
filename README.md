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