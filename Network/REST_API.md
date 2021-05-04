## ✨ REST API?

**RE**presentational
**S**tate
**T**ransfer
어떤말인지 잘 와닿지 않는다..🙄 위키백과의 설명을 살펴보자.

> a way of providing **interoperability** beywen computer systems on the Internet.

컴퓨터의 상호 운용성을 제공하는 방법중 하나라고 써져있다. 여전히 무슨말인지 이해가 잘 안된다.

## 🧾 그럼 REST API의 역사에 대해 알아보자

- 시작 - WEB (1991)
  Q. 어떻게 인터넷에서 정보를 공유할 것인가?
  A. 모-든 정보들을 하이퍼 텍스트로 연결한다.
  정보 표현 형식: HTML
  정보 식별자: URI
  정보 전송방법(프로토콜): HTTP

HTTP를 여러 사람들이 설계하게 되었다. 그중 한 명이 이의를 제기한다.

> How do I improve HTTP without breaking the Web?
> 만약 기존에 구축되어있던 HTTP를 고치면 호환성에 문제가 생기는걸 피하지 않을까?

그럼 어떻게 하면 잘 설계할 수 있을까?
해결책: HTTP Object Model
이 방법은 4년후 REST라는 이름으로 발표가 된다.

### 한편.. API

인터넷 상 API가 만들어질 때, 98년에 XML-RPC라는 이름으로 마이크로소프트에서 프로토콜을 만든다. 이는 SOAP이라는 명칭으로 변경된다. 또 2000년에 Salesforce라는 회사에서 API를 공개하는데, 이는 인터넷에서 최초로 공개된 API중 하나이다. 아래 사진과 같이 굉장히 복잡한 API의 모양이다. 🙄
![](https://images.velog.io/images/yukyung/post/c4993833-1200-448d-9d02-8d1027f6563e/image.png)
잠깐 SOAP API에 대해 알아보자.

> SOAP(Simple Object Access Protocol) 아키텍처는 Open API 환경에서 사용되는 확장성 있는 메시지 프로토콜로, HTTP 통신 프로토콜을 기반으로 XML을 사용하여 데이터를 교환한다. HTTP 프로토콜 사용으로 API 사용자의 접근성이 뛰어나며, XML 형식으로 데이터를 표현하기 때문에 태그, 속성 등을 통해 부가정보의 표현이 자유롭다.

~ 그로부터 4년후.. ~ flickr에 API를 만든다. 아까와 비슷한 SOAP 형태로도 공개를 했지만, REST 방식으로도 공개하게 된다. 사실 이는 2000년도 공개된 논문를 그대로 인용한 케이스다. 하지만 사람들이 보기엔 매우 새로워보였다.
![](https://images.velog.io/images/yukyung/post/8d36072b-f700-4b3d-a58e-c4c2e3577ae9/image.png)
일단.. **짧다!** 같은일을 하는 API지만, SOAP에 비해 REST가 훨씬 짧고 간결하게 와닿게 된다.
![](https://images.velog.io/images/yukyung/post/a53a6116-b002-4f3a-9047-e2866b40fa2e/image.png)
이런 느낌은 결론적으로 SOAP에 비해 REST의 인기가 급부상하는 결과를 낳게 된다. 그 후, AWS가 자사 API의 사용량의 85%가 REST임을 밝히고, Salesforce또한 REST API를 추가하게 된다.

### REST의 승리..?인데 CMIS를 곁들인

사람들은 REST API의 승리인 줄 알았으나.. 2008년에 CMIS라는 것이 등장하게 된다.
**CMIS (2008)**

- CMS를 위한 표준
- EMC, IBM, 마이크로소프트 등이 함께 작업
- **REST**바인딩 지원

이걸 본 로이필딩👨‍💼왈:

> CMIS에 REST는 없습니다.

원작자의 눈에서 CMIS는 REST가 아닌것처럼 보이게 된다. 그럼 여기서 REST처럼 보이는 건 뭘까? 한번 가이드라인을 읽어보도록 하자.

### Microsoft REST API Guidelines(2016)

- uri는 https://{serviceRoot}/{collection}/{id} 형식이어야한다
- GET, PUT, DELETE, POST, HEAD, PATCH, OPTIONS를 지원해야한다
- API 버저닝은 Major.minor로 하고 uri에 버전 정보를 포함시킨다
  등등...

이걸 본 로이필딩👨‍💼왈:

> 이것도 REST API 아님. 이건 걍 HTTP API임.
> REST API는 만드시 hypertext-driven 이어야 함. REST API의 최고의 버저닝 전략은 버저닝을 안 하는 것임.

정작 원작자의 의도와는 다른 REST API.. 뭐가문제일까!?

## ❓ 그래서 REST API가 뭘까

REST API는 REST 아키텍쳐 스타일을 따르는 API이다.
그럼 REST는 뭘까?

> 분산 하이퍼 미디어 시스템(예: 웹)을 위한 아키텍쳐 스타일

그럼 아키텍쳐 스타일은 무엇인가?

> 제약조건들의 집합

그래서 이 제약 조건들을 지켜야 REST를 지킨다, 라는 말이 성립된다.

### REST의 제약조건

REST는 아키텍처인 동시에 하이퍼-아키텍처 스타일이다. 이는 아키텍처 스타일이지만, 아키텍처 스타일의 집합이기 때문이다. 때문에 아래 6가지의 스타일로 이루어져 있다.

REST를 구성하는 스타일

- client-server
- stateless
- cache
- **uniform interface**
- layered system
- code-on-demand (optional, 서버에서 코드를 클라이언트에서 보내서 실행할 수 있어야 한다는 뜻. JS)

기본적으로 HTTP 아래에서 API의 조건을 만족하기에, 요즘의 REST API들은 위의 조건들을 잘 지키고 있다. 그러나 **uniform interface**는 잘 만족하지 못하고 있다.

### uniform interface

uniform interface 또한 하나의 스타일이다. 이는 4가지 제약조건으로 이뤄져 있다.

- 리소스가 URI로 식별되어야 한다.
- representations 전송을 통해서 리소스를 조작해야 한다. (리소스를 만들거나, 업데이트하거나, 삭제하거나 할때 메세지에 표현을 담아 전송후 달성하면 된다는 의미)
- **self-descriptive message, 메시지는 스스로를 설명해야 한다.**
- **hypermedia as the engine of application state(HATEOS)**

이때, 오늘날의 REST API들은 위의 굵은 글씨 항목은 지키지 못하고 있다. 그럼 굵은글씨 항목에 대해 알아보자.

- **self-descriptive message, 메시지는 스스로를 설명해야 한다.**
  예)
  `GET / HTTP/1.1`
  단순한 GET 요청 메서드다. 그런데, 이 메세지에 무언가 빠져있다.
  `GET / HTTP/1.1 Host: www.example.org`
  목적지를 추가하면 self-descriptive 해진다. example.org라는 도메인으로 전송된다! 라는 목적지가 표현되어야 한다.

예) 응답메세지
`HTTP/1.1 200 OK [{ "op": "remove", "path": "/a/b/c" }]`
이 또한 self-descriptive하지 않다. 이는 어떤 문법인지 모르기에 해석할 수 없다.
`HTTP/1.1 200 OK Content-Type: application/json [{ "op": "remove", "path": "/a/b/c" }]`
Content-Type을 명시해주면 어떤 타입인지 알 수 있어 파싱이 가능하고, 문법 해석이 가능하기에, self-descriptive 해진다.

그러나 확실한 self-descriptive은 아니다. 왜냐면 이걸 해석해도, "op"와 "path"의 값의 의미를 알 수 없다.
`HTTP/1.1 200 OK Content-Type: application/json-patch+json [{ "op": "remove", "path": "/a/b/c" }]`
json-patch+json이라는 미디어 타입으로 정의해준다. 해당 명세를 찾아가 이해한 후, 이 메세지를 해석하면 메세지의 의미를 이해할 수 있게 된다.

정리하자면, **self-descriptive message는 메세지를 봤을 때 메세지 만으로 온전한 해석이 가능해야 함을 일컫는다.** 요즘의 REST API들은 appication/json 형식으로만 표현되고, 이걸 어떻게 해석해야 하는가- 는 알려주지 않기에 만족하지 않는다.

- **HATEOAS**
  애플리케이션의 상태는 Hyperlink를 이용해 전이되어야 한다.
  예를들어, 웹사이트의 루트에 접근하면 단순한 게시판이 나타난다. 링크를 누르면 글 목록을 보기 위한 HTTP요청을 보내고, 글쓰기 링크를 보내면 form이 나오고, form에 내용을 작성하면 저장을 요청하기 위한 HTTP 요청을 보내교, 저장한 링크를 보면 내가 작성한 글을 보고, 글을 본다음을 보고 목록을 다시 보는.. 이러한 것을 상태를 전이한다고 표현한다.

이 상태의 전이마다 해당 페이지의 링크를 따라가며 전이했기 때문에, 이 애플리케이션은 HATEOAS해진다. html의 경우 HATEOAS하다.

```html
HTTP/1.1 200 OK Content-Type: text/html

<html>
  <head></head>
  <body>
    <a href="/test">test</a>
  </body>
</html>
```

하이퍼링크가 나와있고, 하이퍼링크를 통해 전이가 되므로 HATEOAS가 만족된다.

```JSON
HTTP/1.1 200 OK
Content-Type: application/json
Link: </articles/1>; rel="previous",
      </articles/3>; rel="next;

{
    "title": "The second article",
    "contents": "blah blah..."
}
```

JSON을 통해서도 HATEOAS하게 표현할 수 있다. 하이퍼링크로 연결되어 있는, 다른 리소스를 가르킬 수 있는 기능을 제공하는 헤더이다.

### 그래서 왜 Uniform Interface가 필요한가

**독립적 진화**

- 서버와 클라이언트가 각각 독립적으로 진화한다.
- **서버의 기능이 변경되어도 클라이언트를 업데이트할 필요가 없다,**
-

독립적 진화는 새로운 API가 추가되고 API가 삭제되고 URI가 변화하는 등, 서버의 상태가 변경되어도 클라이언트가 업데이트 할 필요가 없음을 뜻한다. **이는 곧 REST API를 만든 이유로 직결된다. REST API는 독립적인 진화를 달성하는것이 목표이고, 이를 달성하기 위해서는 반드시 Uniform Interface를 지켜야 한다.** Uinform Interface를 만족하지 못하면 REST API라고 할 수 없게 된다.

## 💯 실제로 REST가 지켜지고 있는가

### **웹**

- 웹 페이지를 변경했다고 웹 브라우저를 업데이트 할 필요가 없다.
- 웹 브라우저를 업데이트 했다고 웹 페이지를 변경할 필요가 없다.
- HTTP 명세가 변경되어도 웹은 잘 동작한다.
- HTMl 명세가 변경되어도 웹은 잘 동작한다.

웹은 모범적인 REST API의 사례다. URI가 바뀌든, 내용이 바뀌든 상관 없이 내가 소유한 웹 브라우저는 항상 잘 접근된다. 크롬의 버전을 업그레이드 했다 해서, 기존 브라우저가 접근이 안되거나 하지 않는다. HTTP 명세가 변경되고, 여러 웹사이트가 HTTP 명세를 변경했어도 웹사이트는 무사히 접근된다. HTML이 5.0, 5.1, 5.2..이 계속해서 나와도, 갑자기 웹사이트가 접근이 불가능해 지진 않는다.

물론 페이지가 깨지거나 하는 일은 존재하나. 구형 브라우저로 접속 시, 레이아웃이 깨지는 일은 발생한다. 하지만 최소한의 동작은 가능하다. 아예 접근이 불가능하진 않고, 최소한의 기능이 동작한다.

### 모바일 앱

모바일 앱은 강제 업데이트 하는 경우가 있다. 서버가 변경되었을 때, 클라이언트가 적용할 수 있는 한계가 있다. 언젠가는 업데이트를 계속 해야한다. 이는 자주 일어나는 일이다.

웹에서는 이러한 일이 잘 일어나지 않는다. 웹사이트가 변경되었다고 해서, 브라우저를 업데이트 해야하는 일이 일어나지 않는다. 앱에서 이러한 일이 일어나는 이유는 REST 아키텍처 스타일을 따르지 않는다는 얘기로 볼 수 있다.

### 그러면 웹은 이런 문제를 어떻게 해결했는가

이는 수많은 사람들의 피땀흘린(!) 노력의 결과물이다. W3C Working groups(HTML 제작), IETF Working groups(HTTP 제작), 웹 브라우저 개발자들, 웹 서버 개발자들 등등.. 결과물이다.

예를들어, HTML5 첫 초안 권고안이 나오는데는 6년이 소모됐다. (HTML5 드래프트 2008년 1월, 첫 권고안 2014년 10월)
HTTP/1.1 명세 개정판 작업하는데는 7년이 소모됐다.(HTTP/1.1 명세 세 번째 개정판인 RFC 7230-7235의 작업기간 2007년 12월 - 2014년 6월) 이는 하위 호환성을 깨트리지 않기 위함이다.

이러한 집착의 끝은.. 상호운용성

- Referer 오타지만 안고침, 고치는 순간 웹이 깨짐
- charset 잘못 지은 이름이지만 안 고침, encoding이 올바른 개념이지만 charst이라 작명함. 하지만 고치면 깨짐2
- HTTP 상태코드 416 포기
  HTTP 상태코드가 계속해서 추가되고 있을 때, 예-전에 만들은 만우절 상태코드가 416번을 갖고있음, HTTP가 아니라 무시해도 됐지만, 수많은 서버 구현체들이 이를 구현했다. 그래서 416번 코드 구현을 포기했다. 이는 해당 구현체가 존재하고, 해당 구현체의 상호 운용성도 지켜야 하기 때문이다.
- HTTP/0.9 아직도 지원 (크롬, 파이어폭스)
  이때 크롬에서 0.9를 제거했더니, 일부 프록시에서 오동작 하는 결과가 있었다. 웹을 깨트릴 수 없기 때문에 제거를 포기한다.

### 그래서 REST가 웹의 독립적 진화에 도움을 주었나

REST의 영향

- HTTP에 지속적으로 영향을 줌
- Host 헤더 추가
- 길이 제한을 다루는 방법 명시, 이 또한 REST의 영향
- URI에서 리소스의 정의가 추상적으로 변경됨 (문서의 위치 => 식별하고자 하는 무언가)
- 그외 다수
- HTTP/1.1 명세 최신판에서 REST에 대한 언급이 들어간다. (이건 로이필딩이 HTTP와 URI 명세의 저자중 한명이기 때문..!)

REST는 웹의 독립적 진화에 도움을 주었고, 웹은 독립적으로 진화하고 있다. 성공적...!

## 🤔 그런데 REST API

위에서 언급한대로, 오늘날의 REST API들은 REST 아키텍쳐 스타일을 잘 지키지 않고 있다. 그럼 REST API는 꼭 저 조건을 지켜야 하는것일까?

**네, 지켜야 합니다.** >> 원작자 오피셜

> REST API는 하이퍼텍스트를 포함한 **self-descriptive**한 **uniform interface**을 통해 리소스에 접근하는 API이다.

기존에 믿고있던 SOAP: 복잡, 규칙많음, 어렵다 REST: 단순, 규칙적음, 쉽다 라고 알고있던 명제가 틀리게 된다. 그냥 둘다 어렵다.

### 그럼 꼭 원격 API가 꼭 REST API이어야 할까?

**아니요!**

> 시스템 전체를 통제할 수 있다고 생각하거나, 진화에 관심이 없다면, REST에 대해 따지느라 시간낭비하지 마라.

하지만 오랜시간에 걸쳐 진화하는 시스템을 설계한다면, REST API에 관심을 갖는게 좋을 것이다.

### 그래서 이제 어떻게 하는데

1. REST API 구현하고 REST API라 부르기
2. REST API 구현 포기하고 HTTP API라고 부르기
3. **REST API가 아니지만 그냥 내맘대로 REST API라고 부르기 (현상황)**

1번에 대해 한번 구현을 해보자.

### REST API 구현하고 REST API라 부르기

왜 API는 REST로 구현하기 어려울까?

|              | 흔한 웹 페이지 | HTTP          |
| ------------ | -------------- | ------------- |
| Protocol     | HTTP           | HTTP          |
| 커뮤니케이션 | 사람-기계      | **기계-기계** |
| Media Type   | HTML           | **JSON, XML** |

문제의 원인은 Media Type임을 알 수 있다. 한번 비교해보자.

|                  | HTML           | JSON   |
| ---------------- | -------------- | ------ |
| Hyperlink        | 됨 (a태그 등)  | 정의 X |
| Self-descriptive | 됨 (HTML 명세) | 불완전 |

JSON은 어떻게 파싱하는지, 해석해라까진 정의되어 있지만 그 안의 값에 대한 정의는 되어있지 않다. 의미를 해석하려면 별도의 문서가 존재해야 한다.

한번 코드로 비교해보자.

```HTML
GET /todos HTTP/1.1
Host: example.org

HTTP/1.1 200 OK
Content-Type: text/html

<html>
<body>
<a href="https://todos/1">회사 가기</a>
<a href="https://todos/2">집에 가기</a>
</body>
</html>
```

Self-descriptive한가? (이것만 봐도 해석이 가능한가?)

1. 응답 메세지의 Content-Type, media type 확인 O
2. HTTP 명세, media type이 IANA에 등록됨을 확인하고 설명을 찾을 수 있다.
3. IANA에 나오는 text/html 명세는, 링크에 명세가 적혀 있음.
4. 명세에 모든 태그의 해석 방법이 구체적으로 나와있음, 이를 해석 가능
5. Self-descriptive 하다.

HATEOAS 한가?
`<a>`태그를 이용해 표현한 링크로, 다음 상태로 전이 가능하다. HATEOAS를 만족한다.

```JSON
GET /todos HTTP/1.1
Host: example.org

HTTP/1.1 200 OK
Content-Type: application/json

[
  {"id": 1, "title": "회사 가기"},
  {"id": 2, "title": "집에 가기"}
]
```

Self-descriptive한가? (이것만 봐도 해석이 가능한가?)

1. Content Type과 meida type이 확인 가능하다.
2. media typ이 IANA에 등록됨을 확인 가능
3. IANA에 따라 링크를 찾아가 명세를 해석한다.
4. 명세에 json 문서를 파싱하는 방법이 명시되어 있으므로 성공적으로 파싱!
5. **그러나 "id"의 의미와 "title"의 의미는 알 수 없음.** 온전한 해석 실패.

HATEOAS
다음 상태로 전이할 링크가 없다. 실패

### 진짜 Self-descriptive와 HATEOAS가 독립적 진화에 도움이 될까?

- Self-descriptive
  확장 가능한 커뮤니케이션

서버나 클라이언트가 변경되더라도 오고가는 메세지는 언제나 self-descriptive하므로 언제나 해석 가능하다.

- HATEOAS
  애플리케이션 상태 전이의 late binding

어디서 어디로 전이가 가능한지 미리 결정되지 않는다. 어떤 상태로 전이가 완료되고 나서야 그 다음 전이될 수 있는 상태가 결정된다.
링크는 동적으로 변경될 수 있다.

따라서 REST API가 가능해진다.

### REST API로 고쳐보자.

**방법1. Media Type**

```JSON
GET /todos HTTP/1.1
Host: example.org

HTTP/1.1 200 OK
Content-Type: application/vnd.todos+json //vnd.todos 추가

[
  {"id": 1, "title": "회사 가기"},
  {"id": 2, "title": "집에 가기"}
]
```

1. 미디어 타입을 하나 정의한다.
2. 미디어 타입 문서를 작성한다. 해당 문서에 "id"가 무엇이고 "title"이 무엇인지 의미를 정의한다.
3. 해당 문서를 IANA(모든 미디어타입이 등록된 사이트)에 미디어 타입을 등록한다. 이 떄 만든 문서를 미디어 타입의 명세로 등록한다. (이름, 메일주소, 타입 이름, 서브타입 이름, 필수 파라메터, 선택 파라메터, 인코딩시 고려사항, 보안 고려사항, 호환성 고려사항, 이 미디어 타입을 사용하는 애플리케이션, 추가 정보, 용도)
4. 이제 이 메시지를 보는 사람은 해석 가능하다!

그러나 너무 번거로운 방법이다.

**방법2. Profile**

```JSON
GET /todos HTTP/1.1
Host: example.org

HTTP/1.1 200 OK
Content-Type: application/json
Link: <https://example.org/docs/todos>; rel="profile" // profile 추가

[
  {"id": 1, "title": "회사 가기"},
  {"id": 2, "title": "집에 가기"}
]
```

Profile은 이것의 의미가 무엇인지 문서의 링크를 걸 수 있다.

1. "id"가 뭐고 "title"이 뭔지 의미를 정의한 명세 작성
2. Link 헤더에 profile relation으로 해당 명세를 링크
3. 이제 메세지를 보는 사람은 명세를 찾을 수 있으므로, 이 문서의 의미를 온전히 해석할 수 있다.

단점은,

1. 클라이언트가 Link 헤더와 profile를 이해해야 한다.
2. Content negotiation(클라이언트에 이상이 생겼을 때 서버에서 알아챔)을 할 수 없다. Media Type으로 판단하는게 아닌 Link 헤더만 보고 판단하기 때문.

- HATEOAS 처리하기
  **방법1. data로**

```JSON
GET /todos HTTP/1.1
Host: example.org

HTTP/1.1 200 OK
Content-Type: application/json
Link: <https://example.org/docs/todos>; rel="profile"

[
  {
    "link": "https://example.org/todos/1",
    "title": "회사 가기"
  },
  {
    "link": "https://example.org/todos/2",
    "title": "집에 가기"
  }
]
```

data에 하이퍼링크 표현하기, 이 또한 충분한 방법이다. 단점으로는 해당 링크를 어떻게든 정의해야 한다.

```JSON
GET /todos HTTP/1.1
Host: example.org

HTTP/1.1 200 OK
Content-Type: application/json
Link: <https://example.org/docs/todos>; rel="profile"

{
  "links": {
    "todo": "https://example.org/todos/{id}" // URI 템플릿
  },
  "data": [{
    "id": 1,
    "title": "회사 가기"
  }, {
    "id": 2,
    "title": "집에 가기"
  }]
]
```

URI 템플릿을 정의하는 방법이다. `{id}`안에 "id"의 번호를 입력해 URI를 결졍하다. 단점은 또한 링크를 표현하는 방법을 정의해야 한다.

하이퍼링크를 표현하는 방법을 정의한 명세를 활용

```JSON
GET /todos HTTP/1.1
Host: example.org

HTTP/1.1 200 OK
Content-Type: application/vnd.api+json
Link: <https://example.org/docs/todos>; rel="profile"

{
  "data": [{
    "type": "todo",
    "id": "1",
    "attributes": { "title": "회사 가기" },
    "links": { "self": "http://example.com/todos/1" }
  }, {
    "type": "todo",
    "id": "2",
    "attributes": { "title": "집에 가기" },
    "links": { "self": "http://example.com/todos/2" }
  }]
}
```

이는 기존 API를 많이 고쳐야 한다는 단점이 있다.

**방법2. HTTP 헤더**

```json
POST /todos HTTP/1.1
Content-Type: application/json

{
    "title": "점심 약속"
}

HTTP/1.1 204 No Content
Location: /todos/1 // Location
Link: </todos/>; rel="collection" // Link
```

Link, Location 등의 헤더로 링크를 표현한다. 단점은 정의된 relation만을 활용해야 한다.

### 몇가지 궁금증

- Hyperlink는 반드시 uri여야 하는가?
  **NO!** 어찌됐든 하이퍼링크면 상관없다.
- Media typ 등록은 반드시 해야 하는가?
  **NO!** 로이필딩왈, 저자가 의도한 목적을 이해하면 등록하지 않아도 된다. 그러나 IANA에 등록하면..아무튼 좋다! 왜냐면 Media type을 누구나 쉽게 사용할 수 있고, 이름 충돌을 피할 수 있기 때문이다.

## 👏 정리

- 오늘날 대부분의 "REST API"는 사실 REST를 잘 따르지 않는다.
- REST 제약조건 중 특히 **Self-descriptive**와 **HATEOAS**를 잘 만족 못한다.
- REST는 긴 시간에 걸쳐 진화하는 웹 어플리케이션을 위한 것이다.
- REST 따를지 말지는 설계하는 사람 맘.
- REST 따를거면 **Self-descriptive**와 **HATEOAS**를 만족시켜야 한다.

* Self-descriptive는 custom meida type이나 profile link relation등으로 만족 가능.
* HATEOAS는 HTTP 헤더나 본문에 링크를 담아 만족 가능.

- REST를 따르지 않는다면, 이를 어떻게 부를지 결정해야 한다.

* HTTP API라고 부를 수 있고,
* 그냥 REST API라고 부를수도 있다. (단, 원작자가 싫어한다. 사실 이래도 큰 문제는 없다.)

## 🔗 Refer

https://tv.naver.com/v/2292653
본 내용은 DEVIEW 2017: 그런 REST API로 괜찮은가 발표를 듣고 정리한 내용입니다.
