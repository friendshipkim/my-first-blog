# What is Rest?

[REST, 혹은 REpresentational State Transfer](https://ko.wikipedia.org/wiki/REST) 라는 것은 웹에서 컴퓨터간의 표준을 제공함으로써 시스템간의 소통을 원활하게 하는 아키텍쳐 스타일입니다. REST의 규칙들을 잘 지키는, 우리가 흔히 말하는 RESTful한 시스템들은 서버와 클라이언트의 역할을 확실하게 분리하며 REST의 특징을 따릅니다. 이제부터 이것들이 어떻게 웹에서 서비스를 운영하는데 도움이 되는지, 그리고 REST는 어떤 식으로 요청을 보내고 응답을 받는지 알아보도록 하겠습니다.



## Separation of Client and Server

서버와 클라이언트는 왜 분리되어야 할까요? 한 마디로 말하면 하나의 서버로 다양한 클라이언트에 대응하기 위함입니다. 예전에는 인터넷 컨텐츠를 소비하기 위한 장치가 적었기 때문에 서버가 다양한 형태의 클라이언트에 대응할 필요가 없었습니다. 하지만 요즘은 한대의 서버에 요청을 보내는 클라이언트가 굉장히 다양해졌습니다. 인터넷 브라우져의 종류도 다양해졌고, 스마트폰에서 어떤 OS를 사용하냐에 따라 굉장히 다른 특성을 가집니다. 그래서 예전처럼 각각의 클라이언트에 맞춰서 서버를 구성하는건 거의 불가능한 일이 되었습니다. 하나의 서버가 여러 대의 클라이언트에 대응하기 위해서는 서버가 클라이언트에 잘 정의된 규칙을 알려주고 클라이언트가 이에 맞춰 요청하게 하면 됩니다. 이것이 바로 REST API인 것이죠. 

REST 아키텍처 스타일에서, 서버와 클라이언트의 구현은 독립적으로 이루어지며 서로에 대해 모든 것을 알 필요가 없습니다. 클라이언트 쪽에서의 코드 수정은 서버에 아무런 영향을 주지 않으며 반대도 마찬가지입니다. 이렇게 함으로써 각 사이드의 확장성을 높일 수 있습니다. REST 인터페이스를 사용함으로써 다른 클라이언트들은 똑같은 REST endpoint에 접근하여 똑같은 요청을 보내지만, 다른 응답을 받을 수 있습니다.



## REST 구성

쉽게 말해 REST API는 다음의 세 가지로 구성되어 있습니다. 자세한 내용은 밑에서 설명하도록 하겠습니다.

- **자원(RESOURCE)** - URI 

- **행위(Verb)** - HTTP METHOD

- **표현(Representations)**

  ​

## REST 의 특징

#### 1. Uniform (유니폼 인터페이스)

Uniform Interface는 URI로 지정한 리소스에 대한 조작을 통일되고 한정적인 인터페이스로 수행하는 아키텍처 스타일을 말합니다.

#### 2. Stateless (무상태성)

REST는 무상태성 성격을 갖습니다. 다시 말해 작업을 위한 상태정보를 따로 저장하고 관리하지 않습니다. 세션 정보나 쿠키정보를 별도로 저장하고 관리하지 않기 때문에 API 서버는 들어오는 요청만을 단순히 처리하면 됩니다. 때문에 서비스의 자유도가 높아지고 서버에서 불필요한 정보를 관리하지 않음으로써 구현이 단순해집니다.

#### 3. Cacheable (캐시 가능)

REST의 가장 큰 특징 중 하나는 HTTP라는 기존 웹표준을 그대로 사용하기 때문에, 웹에서 사용하는 기존 인프라를 그대로 활용이 가능합니다. 따라서 HTTP가 가진 캐싱 기능이 적용 가능합니다. HTTP 프로토콜 표준에서 사용하는 Last-Modified태그나 E-Tag를 이용하면 캐싱 구현이 가능합니다.

#### 4. Self-descriptiveness (자체 표현 구조)

REST의 또 다른 큰 특징 중 하나는 REST API 메시지만 보고도 이를 쉽게 이해 할 수 있는 자체 표현 구조로 되어 있다는 것입니다.

#### 5. Client - Server 구조

REST 서버는 API 제공, 클라이언트는 사용자 인증이나 컨텍스트(세션, 로그인 정보)등을 직접 관리하는 구조로 각각의 역할이 확실히 구분되기 때문에 클라이언트와 서버에서 개발해야 할 내용이 명확해지고 서로간 의존성이 줄어들게 됩니다.

#### 6. 계층형 구조

REST 서버는 다중 계층으로 구성될 수 있으며 보안, 로드 밸런싱, 암호화 계층을 추가해 구조상의 유연성을 둘 수 있고 PROXY, 게이트웨이 같은 네트워크 기반의 중간매체를 사용할 수 있게 합니다.



> 이제 실제로 RESTful 인터페이스를 통해 클라이언트와 서버가 어떻게 소통하는지 알아보도록 하겠습니다. REST 아키텍처에서 클라이언트는 자원(resource)를 얻거나 수정하기 위하여 요청을 보내고 서버는 이 요청에 대한 응답을 보냅니다. 요청을 보내고 응답을 보내기 위한 표준 방법은 다음과 같습니다.



## Making Requests

요청은 일반적으로 이런 식으로 구성되어 있습니다. 

- 어떤 작업을 할 것인지를 알려주는 **HTTP Verb**
- 클라이언트 요청에 대한 정보를 담아서 보내는 **header**
- 자원의 경로
- 데이터를 포함한 message body(optional)

### 1. HTTP Verbs

- GET — id로 해당 자원을 조회하고 해당 도큐먼트에 대한 자세한 정보를 가져옵니다.
- POST — 새로운 자원을 생성합니다.
- PUT  — id를 통해 해당 자원에 접근하여 수정합니다.
- DELETE  —  id를 통해 해당 자원에 접근하여 삭제합니다.

### 2. Headers and Accept parameters

요청의 헤더에서 클라이언트는 서버에게 자신이 조회할 수 있는 리소스의 타입을 알려줍니다. 이 정보는 헤더의 `Accept` 필드에 들어 있습니다. 이로써 서버는 클라이언트가 이해할 수 없거나 접근 권한이 없는 데이터를 보내지 않을 수 있습니다. `Accept` 필드에서 어떤 리소스 타입인지를 명시하는 방법으로 MIME Type을 이용합니다. MIME Type에 대한 더 자세한 정보는 [여기](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types)를 참고하시면 됩니다.  MIME Type은 `type` 과 `subtype`으로 구성되어 있으며 슬래시(/)를 통해 구분됩니다. 

예를 들어, HTML 형식을 포함하는 텍스트 파일은 `text/html` 타입이 됩니다. 만약 이 파일이 HTML 대신에 CSS 형식을 포함하고 있다면 타입은 `text/css` 가 되겠죠. 또한 일반적인 텍스트 파일은 `text/plain` 타입으로 표현됩니다.  하지`text/plain` 타입은 모든 타입을 포괄하지 않습니다. 만약 클라이언트가 얻고 싶은 리소스가 `text/css` 였는데 `text/plain` 를 받았다면 그 내용을 인식하지 못하게 됩니다. 

흔히 쓰이는 `type`과 `subtype`의 예시입니다.

- `image` — `image/png`, `image/jpeg`, `image/gif`
- `audio`  — `audio/wav`, `image/mpeg`
- `video` — `video/mp4`, `video/ogg`
- `application`  — `application/json`, `application/pdf`, `application/xml`, `application/octet-stream`

예를 들어, 클라이언트가 `articles` 안의 `id`가 23번인 리소스에 접근하기 위해서는 서버에 다음과 같은 GET 요청을 보낼 것입니다.

```
GET /articles/23
Accept: text/html, application/xhtml
```

이 때의 `Accept` 헤더 필드는 클라이언트가 `text/html` 또는 `application/xhtml` 두 개의 문서를 받을 수 있다는 것을 알려줍니다.

### 3. Paths

요청은 해당 자원의 경로를 포함하게 됩니다. RESTful API에서 클라이언트는 어떤 자원에 접근하고 있고, 어떤 작업을 하고 있는지 경로를 통하여 쉽게 알 수 있어야 합니다. 보통 경로의 첫 부분은 복수 형태로 작성합니다. 이렇게 함으로써 nested path를 이해하기 쉽게 표현할 수 있습니다.

예를 들어 `fashionboutique.com/customers/223/orders/12` 라는 경로가 있다고 가정해 봅시다. 여러분은 이런 경로를 본 적이 없더라도 이것이 어떤 의미인지 쉽게 파악하실 수 있을 것입니다. 이 경로는 223번 고객의 12번 주문 리소스에 접근하는 경로입니다.

또한 경로는 자원을 얼마나 자세하게 찾을 것인지를 지정합니다.  만약 customer 자원의 리스트를 얻고 싶다면 `fashionboutique.com/customers` 의 경로 뒤에 따로 `id`를 지정할 필요가 없습니다. 하지만 하나의 특정 자원에 접근하고 싶다면 이 경로 뒤에 따로 `id`를 지정해줘야 합니다. 예를 들어 `GET fashionboutique.com/customers/:id` 경로를 통하여 클라이언트는 `customers` 자원에서 주어진 `id`에 해당하는 아이템을 조회하게 됩니다.



## Sending Responses

### 1. Content Types

이번에는 클라이언트에서 요청이 왔을 때, 서버가 응답을 보내는 경우를 생각해 봅시다. 서버는 응답의  헤더에 `content-type`을 포함해야 합니다. `content-type` header field는 클라이언트에게 보낼 데이터의 타입을 명시합니다. 이 데이터 타입은 요청 헤더와 마찬가지로 MIME Type으로 표현됩니다. 응답에서 보내는 `content-type`은 요청으로 들어왔던 `accept` 필드 중의 하나를 포함해야 합니다. 

예를 들어 보겠습니다. 클라이언트가 `article`에서 `id`가 23인 자원을 조회하고 싶을 때, GET 요청은 다음과 같습니다.

```
GET /articles/23 HTTP/1.1
Accept: text/html, application/xhtml
```

그럼 서버는 다음과 같은 응답을 보냅니다.

```
HTTP/1.1 200 (OK)
Content-Type: text/html
```

이는 클라이언트가 요청한 `text/html` 파일을 응답 바디에 넣어서 보낸다는 의미입니다. 클라이언트가 요청했던 `text/html`, '`application/xhtml` 중 하나인 것을 볼 수 있습니다.

### 2. Response Codes

서버가 보내는 응답은 상태 코드를 포함하게 됩니다. 상태 코드는 클라이언트가 요청한 동작이 성공했는지를 알려줍니다. 굉장히 다양한 상태 코드가 있기 때문에  자세한 내용은 [이곳](https://www.codecademy.com/articles/”http://www.restapitutorial.com/httpstatuscodes.html”)을 참고하시면 좋을 것 같습니다. 여기서는  가장 많이 쓰이는 몇 개만 정리해 보도록 하겠습니다.

| 상태 코드                       | 의미                                       |
| --------------------------- | ---------------------------------------- |
| 200 (OK)                    | 클라이언트의 요청을 정상적으로 수행함                     |
| 201 (CREATED)               | 클라이언트가 어떠한 리소스 생성을 요청, 해당 리소스가 성공적으로 생성됨(POST를 통한 리소스 생성 작업 시) |
| 204 (NO CONTENT)            | 클라이언트의 요청을 정상적으로 수행하였지만 응답 바디에 반환되는 내용이 없음 |
| 400 (BAD REQUEST)           | 클라이언트의 요청이 수행될 수 없음(문법 오류, 용량 초과 혹은 다른 클라이언트 오류로 인함) |
| 403 (FORBIDDEN)             | 클라이언트가 이 리소스에 접근할 권한이 없음                 |
| 404 (NOT FOUND)             | 리소스를 찾을 수 없음                             |
| 500 (INTERNAL SERVER ERROR) | 서버에 예상하지 못한 문제가 발생                       |

각각의 HTTP verb에 대하여 요청이 성공적으로 수행되었을 때 서버에서 보내는 응답 코드는 다음과 같습니다. 

- GET — return 200 (OK)
- POST — return 201 (CREATED)
- PUT  — return 200 (OK)
- DELETE  — return 204 (NO CONTENT)



## REST API Design Guide

실제로 REST API를 설계할 때에는 다음과 같은 점을 주의해야 합니다.

#### 1. 슬래시 구분자(/)는 계층 관계를 나타내는 데 사용한다

```
http://restapi.example.com/houses/apartments
http://restapi.example.com/animals/mammals/whales
```

#### 2. URI 마지막 문자로 슬래시(/)를 포함하지 않는다

URI에 포함되는 모든 글자는 리소스의 유일한 식별자로 사용되어야 하며 URI가 다르다는 것은 리소스가 다르다는 것이고, 역으로 리소스가 다르면 URI도 달라져야 합니다. REST API는 분명한 URI를 만들어 통신을 해야 하기 때문에 혼동을 주지 않도록 URI 경로의 마지막에는 슬래시(/)를 사용하지 않습니다.

```
http://restapi.example.com/houses/apartments/ (X)
http://restapi.example.com/houses/apartments  (0)
```

#### 3. 하이픈(-)은 URI 가독성을 높이는데 사용한다

URI를 쉽게 읽고 해석하기 위해, 불가피하게 긴 URI경로를 사용하게 된다면 하이픈을 사용해 가독성을 높일 수 있습니다.

#### 4. 밑줄(_)은 URI에 사용하지 않는다.

글꼴에 따라 다르긴 하지만 밑줄은 보기 어렵거나 밑줄 때문에 문자가 가려지기도 합니다. 이런 문제를 피하기 위해 밑줄 대신 하이픈(-)을 사용하는 것이 좋습니다.

#### 5. URI 경로에는 소문자가 적합하다.

URI 경로에 대문자 사용은 피하도록 해야 합니다. 대소문자에 따라 다른 리소스로 인식하게 되기 때문입니다. RFC 3986(URI 문법 형식)은 URI 스키마와 호스트를 제외하고는 대소문자를 구별하도록 규정하기 때문입니다.

```
RFC 3986 is the URI (Unified Resource Identifier) Syntax document
```

#### 6. 파일 확장자는 URI에 포함시키지 않는다.

```
http://restapi.example.com/members/soccer/345/photo.jpg (X)
```

REST API에서는 메시지 바디 내용의 포맷을 나타내기 위한 파일 확장자를 URI 안에 포함시키지 않습니다. Accept header를 사용하도록 합시다.

```
GET / members/soccer/345/photo HTTP/1.1 Host: restapi.example.com Accept: image/jpg
```



### Reference

http://jaweb.tistory.com/entry/REST-RestFul이란-무엇인가

http://meetup.toast.com/posts/92

https://www.codecademy.com/articles/what-is-rest?utm_source=customer_io&utm_campaign=api_2_13_18&utm_medium=email&utm_term=a&utm_content=inline_link