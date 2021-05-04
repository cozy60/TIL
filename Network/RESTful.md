## ✨ REST API - Representational State Transfer API

REST API에 대한 역사는 <a href="">여기</a>를 참고하도록 한다.
REST API는 소프트웨어 아키텍처가 아닌 아키텍처 스타일이다.

### REST 구성

1. 자원(Resource), URI
   모든 자원의 고유한 ID
   HTTP에서 이러한 자원을 구별하는 ID는 'Students/1'같은 HTTP URI다.

2. 행위(Verb), HTTP METHOD
   URI를 이용해 자원을 지정하고 조작하기 위해 HTTP METHOD (GET, POST, PUT, DELETE..)와 같은 METHOD

3. 표현 (Representation)
   클라이언트가 서버로 요청을 보낼 시 서버가 응답으로 주는 자원, Reresentation
   JSON, XML, TEXT등 여러 형태로 나타낼 수 있다.

> 즉 REST는 URI를 통해 자원을 표시하고, HTTP METHOD를 이용해 자원을 요청하고 그 결과를 받는것

### REST 특징

REST의 특징은 다음과 같다.

1. uniform interface
   URI로 지정한 리소스에 대한 조작을 통일하고 한정적인 인터페이스로 수행하는 아키텍처 스타일
2. stateless
   REST는 상태정보를 따로 저장하고 관리하지 않는다. 세션 정보나 쿠키 정보를 별도로 저장하고 관리하지 않기에 API 서버는 들어오는 요청만을 단순히 처리하면 된다. 이로인해 구현이 단순해진다.
3. cacheable
   REST는 HTTP 웹표준을 그대로 사용하기 때문에, 웹에서 사용하는 기존 인프라를 사용하 수 있다. 따라서 HTTP의 캐싱 기능이나, HTTP 프로토콜 표준에서 사용하는 태그를 사용할 수 있다.
4. self-descriptiveness
   동사(Method) + 명사(URI) 로 이루어져있어 어떤 메서드에 무슨 행위를 하는지 알 수 있다. REST API 메세지만 보고도 쉽게 이해가 가능하다.
5. Client - Server 구조
   REST 서버는 각각의 역할이 확실히 구분된다(자원: Server,자원 요청: Client). 서로간의 의존성이 줄어들고, 관심사를 분리해 각각의 독립적인 진화를 지원해야 한다.
6. 계층형 구조
   REST 서버는 다중 계층으로 구성될 수 있으며 구조상 유연성을 둘 수 있고 중간매체를 사용할 수 있다.

## 💻 REST API 설계

### 설계 규칙

1. API는 HTTP를 전송 계층으로 사용해야 한다.

2. 모든 URI는 명사로 구성되어야 한다. 자원에 대한 행위는 HTTP METHOD로 표현한다.

3. HTTP 상태코드는 정의된 목적에 따라서 모든 응답에 사용되어야 한다. 성공은 모두 200, 실패는 모두 500으로 사용하는 행위는 REST 사상에도 어긋나고, 자기 서술성에도 어긋난다.

4. 슬래시 `/`는 계층 관계를 나타내는데 사용한다.

```
http://restapi.example.com/houses/apartments
http://restapi.example.com/animals/mammals/whales
```

3. 집합, 소속 등 자원의 계층관계를 사용하는 경우 복수형 명사를 사용한다.

```
https://www.apisample.com/users/alice
```

5. 마지막 문자로 슬래시`/`를 포함하지 않는다.

```
http://restapi.example.com/houses/apartments/ (X)
http://restapi.example.com/houses/apartments  (0)
```

6. 하이픈`-`은 URI 가독성을 높이는데 사용한다.

7. 밑줄 `_`은 URI를 사용하지 않는다. (보기 어려움, 가독성 저하)

8. URI 경로에는 소문자가 적합하다. 대문자는 피해야 한다.

9. 파일 확장자는 URI에 포함하지 않는다. Accept header를 사용하도록 한다

```
http://restapi.example.com/members/soccer/345/photo.jpg (X)
```

10. GET이나 POST를 이용한 터널링은 하지 않는다. 이는 Self-descriptiveness 하지 않는다.

```
http://myweb/users?method=update&id=terry
```

11. 요청이나 응답에 대한 형식은 Content-Type 헤더로 정의해야 한다.

12. 언어
    언어별로 다른 URI를 갖는 서비스는 좋지못한 설계이다. Requst Header의 `Accpt-Language`로 받고자 하는 언어를 명시하자. 해당 Header를 참조해 그에 걸맞은 언어를 제공하도록 한다.
    > 한국어로 작성된 컨텐츠를 보고 있는 중 해당 콘텐츠를 미국인 친구에게 보여줄 일이 생겼다고 가정해봅시다. 단순히 URI를 복사해서 주는 것으로는 미국인 친구에게 내가 보고 있는 정보를 제대로 전달해줄 수 없다면 아주 불편할 것입니다.

하지만 이 방법은 자신의 주 언어와 다른 세팅을 갖고 서비스를 이용하는 사용자도 있고, 특정 순간에 특정 언어로 정해 보고싶은 경우도 있다.

> 보통은 Accept-Language보다 우선해서 적용하는 언어 옵션을 세션에 저장할 수 있게 하고, 이에 대한 변경 인터페이스를 서비스에서 제공해주는 식으로 문제를 해결할 수 있습니다.

### 설계시 주의사항

REST API 설계 시 가장 중요한 항목은 아래 두가지 항목이다.

**1. URI는 정보의 자원을 표현해야 한다.**
**2. 자원에 대한 행위는 HTTP MTHOD(GET, POST, PUT, DELETE)로 표현한다.**

👎 Anti pattern

```
GET /users/show/1
```

이 URI은 자원을 표현해야 하는 URI에 `/show/` 같은 불필요한 표현이 들어가 있기 때문에 적절하지 않다. *본다*는 것은 **GET이라는 HTTP Method**로 충분히 표현할 수 있기 때문이다.

```
GET /members/delete/1
```

이 또한 REST를 제대로 적용하지 않은 URI이다.

**URI는 자원을 표현하는데 중점을 두어야 한다.** 행위에 대한 표현이 들어가서는 안된다. (자원의 이름은 **동사보다 명사**를 사용해야 한다.)

👍 Best pattern

```
GET /users/1
```

```
DELETE /members/1
```

위의 잘못된 URI를 수정하면 다음과 같다. **행위를 표현하고자 할때는 HTTP METHOD**를 사용해야 한다. URI에 자원의 행위에 대한 표현이 들어가지 않는 대신, HTTP METHOD를 사용해야 한다. 아래는 REST 설계 방식에서 사용되는 API이다.

| METHOD | 역할                                                   |
| ------ | ------------------------------------------------------ |
| POST   | POST를 통해 해당 URI를 요청하면 **리소스를 생성**한다. |
| GET    | GET을 통해 해당 **리소스를 조회**한다.                 |
| PUT    | PUT을 통해 해당 **리소스를 수정**한다.                 |
| DELETE | GET을 통해 해당 **리소스를 삭제**한다.                 |

이외에 PATCH 라는 METHOD도 존재한다. PATCH PUT과 같이 리소스를 수정한다는 의미이지만, PATCH는 **일부를 변경(부분적으로 업데이트)한다는** 의미이다.

URI는 자원을 표하는데 집중하고,
행위에 대한 정의는 HTTP METHOD를 통해 하는것이 REST API를 설계하는 중심 규칙이다.

### 예시

- 리소스 정보 검색

```
GET /resource
```

- 특정 리소스 정보 검색

```
GET /resource/1
```

- 기존에 존재하지 않는 새로운 리소스 추가

```
POST /resource
```

- 기존애 존재하는 새로운 리소스 업데이트

```
PUT /resource
```

- 기존 리소스를 부분적으로 업데이트

```
PATCH /resource
```

- 기존 리소스 삭제

```
DELETE /resource
```

- 리소스 정보 검색

```
GET /resource
```

### 왜 위의 항목이 지켜지지 않는걸까?

1. 자원에 대한 행위를 URI를 포함하기
   일부 클라이언트에선 PUT과 DELETE 요청을 생성할 수 없다. 또한 특정한 방화벽들은 PUT과 DELETE 요청을 차단해버린다. 그러므로 API는 HTTP POST나 GET을 통해 모든
   요청을 수락하고, URI에 동사를 포함한다. 예를 들어 사용자 124를 삭제하려는 경우, DELETE를 사용하지 않고 POST를 사용할 때 아래와 같은 URI가 나타나게 된다.

```
/users/124?method=delete // Not RESTful, POST METHOD
```

또한 HTML form에서도 PUT과 DELETE를 적용하지 않는다. 이에 대한 의문에 따른 <a href="http://haah.kr/2017/05/23/rest-http-method-in-html-form/">아래와 같은 의견</a>을 살펴 볼 수 있다.

> - Form은 서버에 정보를 제출하기 위해 존재한다

- GET과 POST는 form에 존재하는 대화형 컨트롤에 입력된 값을 보낸다

2. HATEOAS
   오늘날의 API는 대부분 HATEOAS를 존중하지 않는다. 이는 대부분의 응답 형식이 XML과 JSON으로 이뤄지는데, 두 형식 다 하이퍼링크를 전달하는 고유방식을 지원하지 않는다.
   HATEOAS를 API에 적용하면, Self-Descriptive 특성이 더욱 확실해지고 가독성이 증가한다. 그러나 다른 리소스 URI에 대해 의존성을 가지고, 구현이 까다로워진다는 단점이 존재한다.
   이 문제를 해결하기 위해 응답 객체에 해당 리소스의 상태가 전이될 수 있는 link들을 함께 제공한다. link들을 통해 리소스의 다음 상태 전이 정보를 동적으로 제공한다.

```JSON
{
  "rel": "self",
  "href": "http://api.test.com/users/1",
  "method": "GET"
}
```

<a href="https://velog.io/@yukyung/REST-API#rest-api-%EA%B5%AC%ED%98%84%ED%95%98%EA%B3%A0-rest-api%EB%9D%BC-%EB%B6%80%EB%A5%B4%EA%B8%B0">다른 방법</a>으론 Media Type을 정의하고, 문서를 IANA 명세로 등록하는 방법이나 Profile을 사용하는 방법이 있다.

### API 버전 관리

로이 필딩은 <a href="https://www.slideshare.net/evolve_conference/201308-fielding-evolve/31">최고의 REST API 버전 관리 방법은 버전 관리를 하지 않는것</a>이라고 답했었다. REST는, 웹을 중단하지 않고 HTTP를 업데이트 하기 위해 나타난 방법론이다. 이는 API의 버전을 변경할때마다 URL을 변경하지 않는다는 의미로 연결된다고 볼 수 있다. 이러한 견해로 인해 버전 관리 부분에선 여러 <a href="https://news.ycombinator.com/item?id=16680817">논쟁</a>이 발생되어 있다.
하지만 API는 완전히 안정적일 수 없고, 변화를 피할 수 없다. API 버전을 지정하면, 잘못된 요청과 응답에 대해 예방할 수 있고 API 버전 전환을 원활하게 수행할 수 있다. 그러면 API 버전을 어떻게 지정해야 하는지, URL에 포함해야 하는지 아니면 헤더에 정보를 관리해야하는지 등의 고민이 깊어진다.

```
// URI에 버전 정보 넣기, 자원을 식별하는 URI에 버전 정보 추가
https://adventure-works.com/v1/customers/1
https://adventure-works.com/v2/customers/1

// 쿼리 문자열 내 매개변수로 버전 지정하기
https://adventure-works.com/customers/1?version=1
https://adventure-works.com/customers/1?version=2

// 오래된 버전의 경우, 리다렉션을 나타내는 30x 상태코드와 함께 반환한다.
// 301: 이동됨, 302: 일시적으로 다른 위치에 있음. 클라이언트에 계속 사용해서 알리고자 할때 사용
```

```
// 헤더에 버전 정보 넣기

// 커스텀 헤더
GET https://adventure-works.com/customers/3 HTTP/1.1
Custom-Header: api-version=1

// Accept / Content-Type
GET /user/1 HTTP/1.1
Host: myapplication.com
Accept: application/json; version=1

// `vnd.`는 Vendor MIME Type으로,
// 서비스 개발자가 자신의 독자적인 포맷을 규정할 수 있게 HTTP 표준에서 제공하는 접두어 이다.
// `vnd.`이후 서비스 제공자 이름을 쓰고, `+`로 문서의 기본 포맷을 제공한다.
GET /user/1 HTTP/1.1
Host: myapplication.com
Accept: application/vnd.myapplication.user.v1+json
```

각각의 방법은 <a href="https://blog.allegro.tech/2015/01/Content-headers-or-how-to-version-api.html">각각의 장/단점</a>이 존재한다.

```
{servicename}/{version}/{REST URL}
example) api.server.com/account/v2.0/groups
```

<a href="https://bcho.tistory.com/954?category=252770">조대협</a>님은 위와 같은 방법으로 버전 관리를 권장한다고 하셨다.

### 페이징

리소스에 대한 응답에서 모든 필드를 사용하지 않는 케이스가 있다. 이렇게 필드를 제한하는 것은 네트워크 대역폭을 절약할 수 있고, 파싱을 간략화 할 수 있다.
`limit`이나 `rpp`(Record per page, 페이지당 레코드 수), `count`등을 사용하는 방법이 있다.

```
//100번쨰 레코드부터 125번째 레코드까지
/record?offset=100&limit=25
/record?page=5&rpp=25
/record?start=50&count=25
```

페이징을 사용할 경우 Link header와 커스텀 헤더를 사용할 수 있다.

```
HTTP/1.1 200
Pagination-Count: 100
Pagination-Page: 5
Pagination-Limit: 20
Content-Type: application/json
```

HATEOAS를 사용해서 페이징을 처리할 수도 있다.

```JSON
{
  [
    {
      "id":"user1",
      "name":"terry"
    },
    {
      "id":"user2",
      "name":"carry"
    }
  ],
  "links":[
    // 전후 페이지에 대한 링크 제공
    {
      "rel":"pre_page",
      "href":"http://xxx/users?offset=6&limit=5"
    },
    {
      "rel":"next_page",
      "href":"http://xxx/users?offset=11&limit=5"
    }
  ]
}
```

## 🔗 Refer

https://bcho.tistory.com/954?category=252770
https://www.vinaysahni.com/best-practices-for-a-pragmatic-restful-api#method-override
https://docs.microsoft.com/ko-kr/azure/architecture/best-practices/api-design#versioning-a-restful-web-api
https://sanghaklee.tistory.com/57
https://meetup.toast.com/posts/92
https://spoqa.github.io/2012/02/27/rest-introduction.html
https://medium.com/@trevorhreed/you-re-api-isn-t-restful-and-that-s-good-b2662079cf0e
