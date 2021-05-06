## 🤔 멱등성

동일한 요청을 한 번 보내는 것과 여러 번 연속으로 보내는 것이 같은 효과를 갖고, 서버 상태도 동일하게 남을때 HTTP 메서드가 멱등성을 가졌다고 한다.

풀어서 얘기하면, 요청을 몇번 보내든 같은 결과값을 반환하고 서버는 이러한 요청에 대한 상태가 단일 요청과 동일하다는 뜻이다. 아무리 사용자가 서버에 어떠한 요청을, 몇번의 횟수를 요청하든 결과값의 성질이 달라지지 않는다.

멱등성 메서드에는 통계 기록 등을 제외하고선 어떤 부수효과도 존재해서는 안된다.

모든 안전한(서버 상태를 변경하지 않음, 읽기 전용으로 이뤄짐. GET이나 HEAD)메서드는 멱등성을 갖는다.

| HTTP METHOD | 멱등성 여부 |
| ----------- | ----------- |
| POST        | X           |
| GET         | O           |
| HEAD        | O           |
| PUT         | O           |
| DELETE      | O           |

서버는 멱등성을 보장하지 않는다.

### 멱등성 보장

- GET

```
GET /pageX HTTP/1.1
GET /pageX HTTP/1.1
GET /pageX HTTP/1.1
GET /pageX HTTP/1.1
```

`GET /pageX HTTP/1.1`은 멱등성을 갖는다. 여러번 연속해서 호출해도 클라이언트가 받는 응답은 동일하다.

- POST

```
POST /add_row HTTP/1.1
POST /add_row HTTP/1.1   -> Adds a 2nd row
POST /add_row HTTP/1.1   -> Adds a 3rd row
```

`POST /add_row HTTP/1.1`는 멱등성을 가지지 않는다. 여러 번 호출할 경우, 여러 열을 추가한다.

- DELETE

```
DELETE /idX/delete HTTP/1.1   -> Returns 200 if idX exists
DELETE /idX/delete HTTP/1.1   -> Returns 404 as it just got deleted
DELETE /idX/delete HTTP/1.1   -> Returns 404
```

`DELETE /idX/delete HTTP/1.1`는 상태코드마다 응답이 달라질 수 있지만, 멱등성을 보유한다.

## 👀 사담

HTTP 관련 자료를 찾아보다 `Idempotent`라는 단어를 발견했는데, 멱등성이라는 뜻이였다. 멱등성의 정의가 순수함수 프로그래밍에서의 정의와 굉장히 비슷한 부분이 많았는데, 애초에 순수함수가 멱등성의 개념을 내포하고 있었다. 프로그래밍 세계에선 어떠한 값을 보내도 (몇번의 값을 요청해도) 동일한 성질의 결과값이 나타난다는 개념이 두루두루 사용됨을 알게되었다.

## 🔗 Refer

https://developer.mozilla.org/ko/docs/Glossary/Idempotent
