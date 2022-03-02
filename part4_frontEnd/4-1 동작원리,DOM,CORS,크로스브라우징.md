# 브라우저의 동작 원리

1. HTML 마크업을 처리하고 DOM 트리를 빌드한다 => ("__무엇을__" 그릴지 결정)
2. CSS 마크업을 처리하고 CSSOM 트리를 빌드한다 => ("__어떻게__" 그릴지 결정)
3. DOM 및 CSSOM 을 결합하여 렌더링 트리를 형성한다. ("__화면에 그려질 것만__" 결정)
4. 렌더링 트리에서 레이아웃을 실행하여 각 노드의 기하핮거 형태를 계산한다. ("__Box-Model__" 을 생성)
5. 개별 노드를 화면에 페인트한다.



#### Reference

- [Naver D2 - 브라우저의 작동 원리](http://d2.naver.com/helloworld/59361)
- [Web fundamentals - Critical-rendering-path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/?hl=ko)
- [브라우저의 Critical path (한글)](http://m.post.naver.com/viewer/postView.nhn?volumeNo=8431285&memberNo=34176766)



# Document Object Model (DOM)

웹에서는 수많은 이벤트(Event) 가 발생하고 흐른다.

- 브라우저(user agent)로 부터 발생하는 이벤트
- 사용자의 행동(interaction)에 의해 발생하는 이벤트
- DOM의 '변화'로 인해 발생하는 이벤트

발생하는 이벤트는 자바스크립트 객체일 뿐이다. 브라우저의 Event interface에 맞춰 구현된 객체인 것이다. 

여러 DOM Element로 구성된 하나의 웹 페이지는 Window를 최상위로 하는 트리를 생성하게 된다. 결론부터 말하자면 이벤트는 이벤트 각각이 갖게 되는 전파 경로(propagation path)를 따라 전파된다. 그리고 이 전파 경로는 DOM Tree 구조에서 Element의 위상 (hierarchy)에 의해 결정이 된다.

#### Reference

- [스펙 살펴보기: Document Object Model Event](https://jbee.io/web/about-event-in-the-web/)



# CORS

다른 도메인으로부터 리소스가 요청될 경우 해당 리소스는 __cross-origin HTTP 요청__ 에 의해 요청됨. 하지만 대부분의 브라우저들은 보안 상의 이유로 스크립트에서의 cross-origin HTTP 요청을 제한한다. 이것을 `Same-Origin-Policy(동일 근원 정책)`이라고 한다. 요청ㅇ르 보내기 위해서는 요청을 보내고자 하는 대상과 프로토콜도 같아야 하고, 포트도 같아야 함을 의미함.

이러한 문제를 해결하기 위해 과거에는 flash 를 proxy 로 두고 타 도메인간 통신을 했다. 하지만 모바일 운영체제의 등장으로 flash 로는 힘들어졌음.(iOS 는 전혀 flash를 지원 x) 대체제로 나온 기술이 `JSONP(JSON-padding)`이다. jQuery v.1.2 이상부터 `jsonp`형태가 지원되어 ajax를 호출할 때 타 도메인간 호출이 가능. `JSONP`에는 타 도메인간 자원을 공유할 수 있는 몇 가지 태그가 존재함. 예를들어 `img`, `iframe`, `anchor`, `script`, `link`등이 존재한다.

여기서 `CORS`는 타 도메인 간에 자원을 공유할 수 있게 해주는 것이다. `Cross-Origin Resource Sharing` 표준 웹 브라우저가 사용하는 정보를 읽을 수 있도록 허가된 __출처 집합__을 서버에게 알려주도록 허용되는 특정 HTTP 헤터를 추가함으로써 동작한다.

| HTTP Header                      | Description                    |
| -------------------------------- | ------------------------------ |
| Access-Control-Allow-Origin      | 접근 가능한 `url` 설정         |
| Access-Control-Allow-Credentials | 접근 가능한 `쿠키` 설정        |
| Access-Control-Allow-Headers     | 접근 가능한 `헤더` 설정        |
| Access-Control-Allow-Methods     | 접근 가능한 `http method` 설정 |

#### Preflight Request

실제 요청을 보내도 안전한지 판단하귀 위해 preflight 요청을 먼저 보내는 방법을 말한다. 즉 , `Preflight` 는 실제 요청 전에 인증 헤더를 전송하여 서버의 허용 여부를 미리 체크하는 테스트 요청이다. 이 요청으로 트래픽이 증가할 수 있는데 서버의 헤더 설정으로 캐쉬가 가능하다. 서버 측에서는 브라우저가 해당 도메인에서 CORS를 허용하는지 알아보기 위해 preflight 요청을 보내는데 이에 대한 처리가 필요하다. preflight 요청은 HTTP 의 `OPTIONS` 메서드를 사용하며  `Access-Control-Request-*` 형태의 헤더로 전송한다.

이는 브라우저가 강제하며 HTTP `OPTION` 요청 메서드를 이용해 서버로부터 지원 중인 메서드들을 내려 받은 뒤, 서버에서 `approval(승인)` 시에 실제 HTTP 요청 메서드를 이용해 실제 요청을 전송하는 것이다.

#### Reference

- [MDN - HTTP 접근 제어 CORS](https://developer.mozilla.org/ko/docs/Web/HTTP/Access_control_CORS)
- [Cross-Origin-Resource-Sharing 에 대해서](http://homoefficio.github.io/2015/07/21/Cross-Origin-Resource-Sharing/)
- [구루비 - CORS 에 대해서](http://wiki.gurubee.net/display/SWDEV/CORS+(Cross-Origin+Resource+Sharing))



# 크로스 브라우징

웹 표준에 따라 개발을 하여 서로 다른 OS 또는 플랫폼에 대응하는 것을 말한다. 즉, 브라우저의 렌더링 엔진이 다른 경우에 인터넷이 이상없이 구현되도록 하는 기술이다. 웹 사이트를 서로 비슷하게 만들어 어떤 __환경__에서도 이상없이 작동되게 하는데 그 목적이 있다. 즉, 어느 한쪽에 최적화되어 치우치치 않도록 공통요소를 사용하여 웹 페이지를 제작하는 방법을 말한다.



#### Reference

- [크로스 브라우징 이슈에 대응하는 프론트엔드 개발자들의 전략](http://asfirstalways.tistory.com/237)



# 웹 성능과 관련된 Issue 정리

### 1. 네트워크 요청에 빠르게 응답하자

- `3.xx` 리다이렉트를 피할 것
- `meta-refresh` 사용금지
- `CDN(content delivery network)` 을 사용할 것
- 동시 커넥션 수를 최소화 할 것
- 커넥션을 재활용할 것

### 2. 자원을 최소한의 크기로 내려받자

- 777K
- `gzip` 압축을 사용할 것
- `HTML5 App cache`를 활용할 것
- 자원을 캐시 가능하게 할 것
- 조건 요청을 보낼 것

### 3. 효율적인 마크업 구조를 구축하자

- 레거지 IE 모드는 http 헤더를 사용할 것
- @import 사용을 피할 것
- inline 스타일과 embedded 스타일을 피할 것
- 사용하는 스타일만 CSS 에 포함할 것
- 중복되는 코드를 최소화 할 것
- 단일 프레임워크를 사용할 것
- Third Party 스크립트를 삽입하지 말 것

### 4. 미디어 사용을 개선하자

- 이미지 스프라이트를 사용할 것
- 실제 이미지 해상도를 사용할 것
- CSS3를 활용할 것
- 하나의 작은 크기의 이미지는 DataURL을 사용할 것
- 비디오의 미리보기 이미지를 만들 것

### 5. 빠른 자바스크립트 코드를 작성하자

- 코드를 최소화할 것
- 필요할 때만 스크립트를 가져올 것 : flag 사용
- DOM 에 대한 접근을 최소화 할 것 : Dom manipulate 는 느리다.
- 다수의 엘리먼트를 찾을 때는 selector api를 사용할 것
- 마크업의 변경은 한번에 할 것 : temp 변수를 활용
- DOM 의 크기를 작게 유지할 것
- 내장 JSON 메서드를 사용할 것

### 6. 애플리케이션의 작동원리를 알고 있자.

- Timer 사용에 유의할 것.
- `requestAnimatuinFrame`을 사용할 것
- 활성화 될 때를 알고 있을 것



#### Reference

- [HTML5 앱과 웹사이트를 보다 빠르게 하는 50 가지 - yongwoo Jeon](https://www.slideshare.net/mixed/html5-50)
