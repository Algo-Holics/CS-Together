# 01장: HTTP 핵심 기술 및 웹 기초

# **1) 인터넷의 멀티미디어 배달부**

- 신뢰성 있는 데이터 전송 프로토콜을 사용하므로 전송 중 손상되거나 꼬이지 않음이 보장된다.(신뢰성)

‌

# **2) 웹 클라이언트와 서버**

![1](https://gblobscdn.gitbook.com/assets%2F-MRQFpad84L4tUp7A8aB%2F-MXeowxEcLs3ti9XxGLV%2F-MXeq7NrbMwpbhPUCRkB%2F1-0.png?alt=media&token=df37b9da-1490-434c-8c98-8407654d55dd)

‌

# **3) 리소스**

- 웹 서버는 웹 리소스를 관리 및 제공
- 웹 콘텐츠의 원천
- 파일 시스템의 정적 파일 : 텍스트, html, word, jpeg, avi, 등 파일
- 동적 콘텐츠: 사용자에 따라, 요청에 따라, 시간에 따라 다른 콘텐츠 생성

‌

## **① 미디어 타입**

- MIME: Multipurpose Internet Mail Extensions 데이터 포맷 라벨
    - 주타입(primary object type)/부타입(specific subtype)
    - 예
        - HTML : text/html
        - Jpeg: image/jpeg
        - gif: image/gif

‌

## **② URI, URL, URN**

![2](https://gblobscdn.gitbook.com/assets%2F-MRQFpad84L4tUp7A8aB%2F-MXeowxEcLs3ti9XxGLV%2F-MXeq8exvEkkPi19wfWZ%2F1-1.png?alt=media&token=ac56bcd7-6c6f-4f71-8150-cb03133f3dc6)

‌

- **URI**

‌

 웹 서버 리소스를 각자 이름을 갖고 있기 때문에 클라이언트는 관심있는 리소스를 지목할 수 있다.

 서버 리소스 이름을 URI (Uniform Resource Identifier, 통합 자원 식별자)라고 부른다.

 (인터넷 우편물 주소처럼) 정보 리소스를 고유하게 식별하고 위치 지정

‌

- **URL**

    URL (Uniform Resource Locator, 통합 자원 지시자)

    리소스 식별자 중 가장 흔한 형태

    리소스가 적확히 어디있고 어떻게 접근할지 분명히 알려준다.

    세 부분으로 이루어진 표준 포맷을 따른다.

- 스킴: 리소스에 접근하기 위한 프로토콜 서술 (http, ftp, ..)
- 서버의 인터넷 주소(www.google.com, www.naver.com , ...)
- 웹 서버의 리소스(/book/isbn, /member/id, ... )
- **URN**

    URN (Uniform Resource Name)

    리소스의 위치에 영향을 받지 않는 유일무이한 이름의 역할. (위치에 독립적임)

    널리 채택되지는 않았음 (실험 중)

‌

# **4) 트랜잭션**

HTTP 트랜잭션은 요청 명령과 응답 결과로 구성되어있다. **HTTP 메세지**라고 불리는 정형화된 데이터 덩어리로 상호작용한다.

‌

## **① 메서드**

 HTTP 요청 메세지는 한 개의 메서드를 갖는다.

 메서드는 서버에 어떤 동작을 취해야 하는지 말해준다. (예: 웹페이지 가져오기, 게이트 웨이 프로그램 실행하기, 파일 삭제 등)

 종류: GET, POST, PUT, PATCH, DELETE, HEAD

‌

## **② 상태코드**

 HTTP 응답 메세지는 상태코드와 함께 반환. 요청 성공, 추가 조치가 필요한지 여부를 알려주는 3자리 숫자.‌

 사유 구절도 함께 보내주는데, 단지 설명만을 위해 포함.

‌

## **③ 웹페이지는 여러 객체로 이루어질 수 있다.**‌

'웹 페이지'는 보통 하나의 리소스가 아닌, 리소스의 모음이다.

첨부된 리소스들에 대해 각각 별개의 HTTP 트랜잭션을 필요로 한다.

‌

# **5) 메시지**

사람이 읽고 쓰기 편한 일반 텍스트 형식.(단순 줄 단위 텍스트 구조)

![3](https://gblobscdn.gitbook.com/assets%2F-MRQFpad84L4tUp7A8aB%2F-MXeowxEcLs3ti9XxGLV%2F-MXeq9aYTEdXbRA1IKWo%2F1-2.png?alt=media&token=34ae66c1-5fef-4ade-b6e5-846e57b2aa2e)

‌

요청 메시지: 웹 클라이언트에서 웹 서버로 보낸 HTTP 메시지

‌

응답 메시지: 서버에서 클라이언트로 가는 메시지

‌

1. **시작줄**: 요청시 무슨일을 할지, 응답시 무슨일이 일어날지 나타낸다.
2. **헤더**: 0개 이상의 헤더 필드, 쌍점(:) 으로 구분되어 하나의 이름과 값으로 구성. 헤더는 빈 줄(empty line)으로 끝난다.
3. **본문**: 요청본문은 웹서버로 데이터를 실어 보내고, 응답 본문은 클라이언트로 데이터 반환. 
임의의 이진 데이터 포함가능(이미지,비디오,오디오 등) 하며 텍스트도 포함이 가능하다.

‌

# **6) TCP 커넥션**

‌

## **① TCP/IP**

 HTTP 는 애플리케이션 계층 프로토콜.

 네트워크의 핵심 세부사항에 대해서는 신경쓰지 않음. 인터넷 전송 프로토콜인 TCP/IP이 담당

‌

 역할

- 오류 없는 데이터 전송
- 순서에 맞게 전달
- 조각나지 않는 데이터 스트림 (언제든, 어떤 크기든)

‌

## **② 접속, IP주소, 포트 번호**

IP주소와 port 번호를 사용해서 TCP/IP커넥션을 맺어야 한다.

서버 컴퓨터에 대한 IP 주소와 서버에서 실행중인 프로그램이 사용중인 port 번호가 필요
(URL을 이용해서 알 수 있다.)

‌

예

 [http://172.31.103.5:80/index.html](http://172.31.103.5/index.html)

 [http://www.google.com:80/index.html](http://www.google.com/index.html)

 [http://www.google.com/index.html](http://www.google.com/index.html)

‌

IP주소: 172.31.103.5, port번호: 80

호스트명(도메인 이름, IP주소에 대한 이해하기 쉬운 형태의 별명): www.google.com

포트번호 생략시 기본값 80

‌

## **③ 텔넷(Telnet) 사용 예시**

![4](https://gblobscdn.gitbook.com/assets%2F-MRQFpad84L4tUp7A8aB%2F-MXeowxEcLs3ti9XxGLV%2F-MXeqAlKMnp0I9wh0OrE%2F1-3.png?alt=media&token=ba8962d0-d14e-4685-bab2-91ed22f3dc1e)

‌

1. 사용환경 : Mac
2. telnet 설치 후 google 접속해 보았더니 응답메세지로 200 ok 받은 모습
3. 내 노트북의 ip 주소확인 : [https://aroundck.tistory.com/1033](https://aroundck.tistory.com/1033)
4. 내가 보고있는 웹브라우저가 사용중인 프로토콜 찾는 방법: [https://blog.gomgom.net/how-to-check-web-server-protocol/](https://blog.gomgom.net/how-to-check-web-server-protocol/)

‌

# **7) 웹의 구성요소**

‌

- **Proxy(프락시):** 클라이언트와 서버 사이에 위치한 HTTP 중개자 (보안, 애플리케이션 통합, 성능 최적화).주로 보안. 요청 응답 필터링.
- **Cache(캐시)**: 많이 찾는 웹페이지를 클라이언트 가까이에 보관하는 HTTP 창고 (자주 찾는 사본 저장.클라이언트는 멀리 떨어진 웹 서버보다 근처 캐시에서 문서 다운)
- **Gateway(게이트웨이):** 다른 에플리케이션과 연결된 특별한 웹 서버 중재자 (주로 HTTP 트래픽을 다른 프로토콜로 변환)
- **Tunnel(터널):** 단순 Http 통신을 전달하기만 하는 특별한 프락시 (비 HTTP 데이터를 하나이상의 HTTP 로 연결 및 전송)
- **Agent(에이전트):** 자동화된 Http요청을 만드는 준지능적 웹 클라이언트

