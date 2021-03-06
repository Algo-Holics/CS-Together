# CH12: 기본 인증

사용자를 확인하는 기초적인 체계를 중점적으로 다룬다.

어떻게 HTTP 인증이 DB와 동작하는지 알아본다.

---

## 01) 인증

인증이란, 당신이 누구인지 증명하는 것이다. 

완벽한 인증이란 없다. 비밀번호를 누군가 추측하거나, 엿들을수 있고, 도둑맞거나 위조될수 있다.

하지만 여러 데이터는 당신이 누구인지 판단하는데 도움이 된다.

### ① HTTP의 인증요구/응답 프레임워크

HTTP는 사용자 인증을 하는데 사용하는 **자체 인증 요구/응답 프레임워크를 제공**한다.

- 절차
    - 웹 애플이케이션이 HTTP 요청을 받으면 서버는 '인증 요구'로 응답한다.
    [사용자가 누구인지 알 수 있게 개인정보 요구]
    - 사용자가 다시 요청을 보낼때 '인증 정보'를 첨부해야한다.
        - 인증 정보가 맞지 않으면 서버는 클라이언트에 다시 인증요구를 보내거나 에러반환
        - 인증 정보가 맞으면 요청은 문제없이 처리 완료

### ② 인증 프로토콜과 헤더

HTTP는 필요에 따라 고쳐 쓸 수 있는 제어 헤더를 통해서 다른 인증 프로토콜에 맞추어 확장할 수 있는 프레임워크를 제공한다. 인증프로토콜에 따라 헤더의 형식과 내용이 달라질 수 있다. 인증 프로토콜은 HTTP 인증 헤더에 기술되어있다.

[인증 단계 예시]

![02](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fb8f7c1c0-a237-4c0b-b217-c94bb5567c21%2FUntitled.png?table=block&id=9049edcc-f1aa-449b-a49c-5dbe19373c11&spaceId=da06fe4c-dbc0-451e-a09d-8fe561a808ae&width=2220&userId=&cache=v2)

HTTP 에는 **기본 인증**과 **다이제스트 인증** 2가지 공식적인 인증 프로토콜이 있다.

미래에는 사람들이 HTTP 인증요구/응답 프레임워크를 사용해 새로운 프로토콜을 고안할수 있을것이다.

```markdown
[참조]
현대 HTTP 인증요구/응답 프로토콜을 사용하는 인증 프로토콜로는 OAuth가 있다.
OAuth는 모바일 기기같은 다양한 애플리케이션에서 API 인증을 위해 사용하는 최신 인증 프로토콜이다.
```

### ③ 보안 영역

HTTP가 각 리소스마다 다른 접근 조건을 어떻게 다룰까?

웹서버는 기밀문서를 보안영역 `realm` 그룹으로 나눈다. 보안영역은 저마다 다른 사용자 권한을 요구한다.

`realm` 파라미터가 함께 기술된 기본 인증 예

```markdown
HTTP/1.0 401 Unauthorized
WWW-Authenticate: Basic real="Corporate Financials"
```

`realm` 은 회사 재무 같은 형식으로 해설해서 권한의 범위를 이해하는데 도움되어야한다.

[회사 재무 영역만 접근 가능한 권한을 부여한다.]

## 2) 기본 인증

기본 인증은 가장 잘 알려진 HTTP 인증 규약으로, 거의 모든 주요 client-server에 구현되어있다.

기본 인증에서 웹 서버는 클라이언트의 요청을 거부하고, 유효한 사용자이름과 pw를 요구할수있다.(앞서 내용)

### ① 기본인증 예

기본 인증 헤더

- **인증 요구 헤더(server → client)**

```markdown
### 문법
`WWW-Authenticate: Basic real= 따옴표로 감싼 문서 집합 정보`
### 설명
각 사이트는 보안 영역마다 다른 비밀번호가 있고, 
realm은 요청받은 문서집합의 이름을 따옴표로 감싼것으로, 
사용자는 이 정보를 통해 어떤 비밀번호를 사용해야하는지 알 수 있다.
```

- **응답 (client → server)**

```markdown
### 문법
`Authorization: Basic base-64로 인코딩한 사용자이름과 비밀번호`
### 설명
사용자 이름과 비밀번호는 콜론으로 잇고(:),
base-64로 인코딩해서 사용자이름과 비밀번호에 쉽게 국제 문자를 포함할수 있게하고
네트워크 트래픽에 사용자 이름과 비밀번호가 노출되지 않도록한다.
```

### ② Base-64 사용자 이름/비밀번호 인코딩

Base-64 인코딩은 바이너리, 텍스트, 국제문자 데이터 (어떤 시스템에서는 문제를 일으킬 수 있는) 문자열을 받아서 전송할 수 있게, 그 문자열을 전송 가능한 문자인 알파벳으로 변환하기 위해 발명됬다. 전송 중 문자열이 변질될 걱정 없이 원격에서 디코딩 가능하다.

Base-64 인코딩은 국제 문자, HTTP헤더에 사용할수 없는 문자 (큰따옴표, 콜론, 캐리지리턴)를 포함한 사용자 이름과 비밀번호를 보내야할 때 유용할 수 있다. 또한 서버나 네트워크를 관리하면서 뜻하지 않게 사용자 이름과 비밀번호가 노출되는 문제를 예방하는데 큰 도움이 된다.

### ③ 프락시 인증

프락시 서버를 통해 인증할 수도 있다. 어떤 회사는 사용자들이 회사의 서버나 LAN, 무선네트워크에 접근하기 전에 프락시 서버를 거치게 하여 사용자를 인증한다.

프락시 서버에서 접근 정책을 중앙관리할 수 있기 때문에, 회사 리소스 전체에 대해 통합 접근 제어를 하기 위해서 프락시 서버를 사용하면 좋다. 프락시 인증은 웹 서버의 **인증과 헤더**와 **상태코드만** 다르고 **절차는 같다.**

## 3) 기본 인증의 보안 결함

기본 인증은 단순하고 편리하지만 안심할 수 없다.

기본 인증은 악의적이지 않은 누군가가 의도치 않게 리소스에 접근하는 것을 막는데 사용하거나, SSL같은 암호기술과 혼용한다.

다음 보안 결함을 살펴보자.

1. 기본인증은 사용자 이름과 비밀번호를 쉽게 디코딩할 수 있는 형식으로 네트워크에 전송한다.
[이게 문제가 된다면, 모든 HTTP 트랜잭션을 SSL암호화 채널을 통해 보내거나, 보안이 더 강화된 다이제스트 인증 같은 프로토콜을 사용하는게 좋다.]
2. 기본인증은 재전송 공격을 예방하기 위한 어떤 일도 하지 않는다.
3. 악의가 있는 똑독한 누군가가 무료 인터넷 이메일 같은 사이트에서 사용자 이름, pw 를 그대로 캡쳐해서 중요한 온라인 은행사이트에 접근할수도 있다.
4. 메시지 인증헤더 외 다른 부분을 수정해서 트랜잭션의 원래 의도륵 바꿔버리는 중개자(프록시 등)가 개입하면 정상적인 동작을 보장하지 않는다.
5. 가짜 서버 위장에 취약하다.