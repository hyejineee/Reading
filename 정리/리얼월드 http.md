# 리얼월드 HTTP

## 1장. HTTP/1.0의 신택스 : 기본이 되는 네가지 요소 

* http란 무엇인가? 

  * 웹 브라우저와 웹 서버가 통신하는 절차와 형식을 규정한 것
  * 다양한 서비스의 인터페이스로도 사용된다.

* http/0.9의 한계 

  * 하나의 문서를 전송하는 기능밖에 없었다. -> 그럼 현재는 여러가지 문서를 전송할 수 있나?
  * 통신되는 모든 내용은 html 문서로 가정했으므로, 다운로드할 콘텍츠의 형식을 서버가 전달할 수단이 없었다.
  * 클라이언트 쪽에서 검색 이외의 요청을 보낼 수 없었다. 
  * 새로운 문장을 전송하거나 갱신 또는 삭제할 수 없었다.

* http/1.0에서 추가된 내용

  * 요청 시 
    * 메서드 
    * http 메서드 
    * 헤더 
  * 응답 시 
    * http버전과 스테이터스 코드 
    * 헤더 

* 헤더 [헤더 - MDN](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers)

  * 이름 : 값 형태 

  * 본문 이외의 모든 정보를 포함하는 곳 

  * 서버와 클라이언트 사이에 필요한 추가 정보, 지시나 명령, 당부 등을 쓰는 장소 

  * 클라이언트 -> 서버 헤드

    * User-Agent : 클라이언트가 자신의 이름을 넣는 곳 
    * Referer : 서버에서 참고하는 추가 정보. 클라이언특각 요청을 보낼 때 보곡있던 페이지의 URL을 보낸다.
    * Authorization : 특별한 클라이언트에만 통신을 허가할 때 인증 정보를 서버에게 전달. 

  * 서버 -> 클라이언트 

    * Content-Type : 파일의 종류를 지정. MIME 타입이라는 식별자를 기술한다.
    * Content-Length : 바디 크기. 압축이 이루어지는 경우 압축 이후의 크기가 들어간다.
    * Content-Encoding : 압축이 이루어진 경우 압축 형식을 설명
    * Date : 문서 날짜

  * MIME 타입 [MIME - MDN](https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/MIME_types)

    * 클라이언트에게 전송된 문서의 다양성을 알려주기 위한 메커니즘

    * 브라우저들은 리소스를 내려받았을 때 해야할 기본 동작이 무엇인지를 결정하기 위해 대게 MIME 타입을 사용.

    * 구조 :

      * type/ sub type -> text / html 

      * type = 카테고리. 개별 혹은 멀티파트 타입이 될 수 있다. 

        * 멀티파트 타입 : 

          일반저으로 다른 MIME 타입들을 지닌 개별적인 파트들로 나누어지는 문서의 카테고리를 가리킨다. 

          * 합성된 문서를 나타내는 방법 

      * subtype = 각각의 타입에 한정되는 값이 들어간다. 

    * [정확한 MIME타입 설정의 중요성](https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/MIME_types#%EC%A0%95%ED%99%95%ED%95%9C_mime_%ED%83%80%EC%9E%85_%EC%84%A4%EC%A0%95%EC%9D%98_%EC%A4%91%EC%9A%94%EC%84%B1)

    * MIME 스니핑 

      * 브라우저에서 리소스를 훑어보고 정확한 MIME 타입을 추측해내는 것 
      * MIME 타입이 없을 때 혹은 클라이언트가 타입이 잘못 설정됐닥고 판다한 경우에, 브라우저들은 MIME 스니핑을 시도할 수 있다. 
      * 보안의 구멍이 될 수 있다.

* 메서드 ([메서드- MDN](https://developer.mozilla.org/ko/docs/Web/HTTP/Methods))

  * 주어진 리소스에 수행하길 원하는 행동을 나타냄. 리소스에 대한 조작을 서버에 지시.
  * 응답 메서드는 안전하거나, 캐시 가능하거나, 멱등성을 가질 수 있다. 

* 스테이터스 코드 ([스테이터스 코드 - MDN](https://developer.mozilla.org/ko/docs/Web/HTTP/Status))

  * 특정 http 요청에 대한 응답 코드 
  * 1xx : 조건부 응답 - 처리가 계속 됨을 나타낸다.
  * 2xx : 성공 - 성공했을 때의 응답 
  * 3xx : 리다이렉션 
    *  서버에서 클라이언트로의 명령.
    *  오류가 아니라 정상 처리의 범주. 
    *  클라이언트는 요청을 마치기 위해 추가 동작을 취해야 한다. 
    *  클라이언트는 응답의 Location헤더를 보고 해당 주소로 다시 요청한다. 
    *  리다이렉트하는 곳이 다른 서버라면 리다이렉트할 때 마다 TCP세션 접속, HTTP 송수신으로 두 번 왕복 통신이 발생한다. -> 리다이텍트 수가 늘어나면, 그만큼 표시에 걸리는 시간이 늘어난다.
  * 4xx : 요청 오류 (클라이언트 에러) - 클라이언트가 보낸 요청이 오류가 있다.
  * 5xx : 서버 오류 (서버 에러) - 서버 내부에서 오류가 발생했다.

## 2장. HTTP/1.0의 시맨틱스 : 브라우저의 기본 기능의 이면

* 브라우저의 기본 요소 응용, 기본 기능 실현

* 폼 전송 

  * Content-type : 

    * 리소스의 미디어 타입을 나타내기 위해 사용되는 헤더 
    * POST 메서드를 사용하여 서버로 데이터를 보낼 때, 요청 본문의 유형을 나타내는 헤더 

    ---

    참고 : html form 태그의 enctype속성 [w3c](https://www.w3schools.com/tags/att_form_enctype.asp)

    서버로 데이터를 보낼 때 form-data를 어떻게 인코딩할 것인지에 대한 설정 

    ```html
    <form method="post" enctype="multipart/form-data">
      ...
    </form>
    ```

    ---

    * x-www-form-urlencoded [MDN참고](https://developer.mozilla.org/ko/docs/Web/HTTP/Methods/POST)

      * 모든 문자들은 서버로 보내지기 전에 인코딩됨을 명시

      * html에서 form으로 데이터를 전송할 때 enctype을 설정하지 않으면 기본으로 적용되는 값

      * &으로 분리되고 '='으로 값과 키를 연결하는 key-value tuple로 인코딩하는 방법 

      * 알파벳, 수치, 별표, 하이픈, 마침표, 언더스코어를 제외한 문자들은 percent endcoded로 인코딩된다. -> 바이너리 데이터를 사용하기에는 적합하지 않다.

        ```html
        POST / HTTP/1.1
        Host: foo.com
        Content-Type: application/x-www-form-urlencoded
        Content-Length: 13
        
        say=Hi&to=Mom
        ```

    * multipat/form-data [MDN 참고](https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/MIME_types#multipartform-data)

      * 모든 문자를 인코딩하지 않음을 명시
      * 서버로 파일이나 이미지를 전송할 때 사용하는 인코딩 방법
      *  multipart를 이용하는 경우 한 번의 요청으로 복수의 파일을 전송할 수 있다.
        * 받는 쪽에서는 boundary를 통해 파트를 구분한다.
        * boundary는 각 브라우저가 독자저인 포맷으로 랜덤하게 만든다. 
      * 항목마다 추가 메타 정보를 태그로 가질 수 있다.

      ```html
      <form action="http://localhost:8000/" method="post" enctype="multipart/form-data">
        <input type="text" name="myTextField">
        <input type="checkbox" name="myCheckBox">Check</input>
        <input type="file" name="myFile">
        <button>Send the file</button>
      </form>
      
      
      POST / HTTP/1.1
      Host: localhost:8000
      User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:50.0) Gecko/20100101 Firefox/50.0
      Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
      Accept-Language: en-US,en;q=0.5
      Accept-Encoding: gzip, deflate
      Connection: keep-alive
      Upgrade-Insecure-Requests: 1
      Content-Type: multipart/form-data; boundary=---------------------------8721656041911415653955004498
      Content-Length: 465
      
      -----------------------------8721656041911415653955004498
      Content-Disposition: form-data; name="myTextField"
      
      Test
      -----------------------------8721656041911415653955004498
      Content-Disposition: form-data; name="myCheckBox"
      
      on
      -----------------------------8721656041911415653955004498
      Content-Disposition: form-data; name="myFile"; filename="test.txt"
      Content-Type: text/plain
      
      Simple file.
      -----------------------------8721656041911415653955004498--
      ```

* 컨텐츠 협상 [Content negotiation - MDN](https://developer.mozilla.org/ko/docs/Web/HTTP/Content_negotiation)
  * 동일한 URI에서 리소스의 서로 다른 버전을 서브하기 위해 사용되는 메커니즘 
  * 클라이언트에 적합한 리소스를 제공하기 위한 구조 (언어, 이미지 포맷, 인코딩 등등)
  * 협상 대상
    * MIME 타입 (Accept / Content-type )
    * 언어 (Accept-Language / Content-Language, html 태그)
    * 문자셋 (Accept-Charset / Content-Type)
      * 바디 압축(Accept-Encoding / Content-Encoding)
  * 협상 방식 (참고 : 그림으로 배우는 http & network basic)
    1. 클라이언트가 보내는 HTTP 헤더를 이용하는 방법 (서버 구동형 또는 서버 주도 협상)	
       * 서버 측에서 콘텐츠 협상을 하는 방법
       * 서버 측에서 요청 헤더 필드의 정보를 참고해서 자동적으로 처리 
       * 한계
         * 서버는 클라이언트의 모든 정보를 알고 있지 않음. -> 선택한 리소스가 클라이언트에 적합하지 않을 수도 있음
         * 클라이언트의 정보가 많음 -> 메시지의 크기가 커짐.
         * 캐식가 덜 효율적일 수 있음. 서버 구현이 복잡해짐
    2. 서버에 의해 전달되는 HTTP응답 코드를 이용하는 방법 (에이전트 구동형 또는 에이전트 주도 협상)
       * 클라이언트 측에서 콘텐츠 협상을 하는 방법
       * 브라우저에 표시된 선택지 중에서 유저가 수동으로 선택 
       * 한계 
         * 실제 리소스를 가져오는데 한 개 이상의 요청을 필요로 함 -> 리소스 효용이 떨어짐
         * HTTP표준에서 이 과정을 자동화 하는 방법을 막음 -> 거의 리다이렉션과 함께 사용됨
    3. 트랜스페어런트 네고시에이션 
       * 서버 구동형과 에이전트 구동형을 혼합한 것으로 서버와 클라이언특가 각각 콘텐츠 협상하는 방법
* 쿠키 [쿠키 - mdn](https://developer.mozilla.org/ko/docs/Web/HTTP/Cookies)
  * 웹사이트의 정보를 저장하는 작은 파일. 서버가 웹브라우저에 전송하는 작은 데이터 조각.(서버가 클라이언트에 쿠키 저장을 지시)
  * 주로 요청이 동일한 브아우저에서 들어왔는지 아닌지 판단할 때 주로 사용한다. 
  * 상태 정보를 유지할 수 있음. (http는 기본적으로 스테이트리스 프로토콜)
  * 쿠키의 목적
    * 세션 관리 : 서버에 저장해야 할 로그인, 장바구니, 게임 스코어 등의 정보 관리 
    * 개인화 : 사용자 선호, 테마 등의 세팅
    * 트래킹 : 사용자의 행동을 기록하고 분석하는 용도
  * 쿠키의 잘못된 사용법
    * 영속성 문제 
      * 쿠키가 어떤 상황에서도 확실하게 저장되는 것은 아님.
      * 비밀 모드 혹은 브라우저의 보안 설정에 따라 세션이 끝나면 초기화되거나 쿠키를 보관하라는 서버의 지시를 무시할 수 있음.
    * 용량 문제
      * 쿠키의 최대 크기는 4킬로 바이트.
    * 보안 문제 
      * HTTP 통신에서는 쿠키가 평문으로 전송됨.
      * 원리상 사용자가 쿠키를 수정하는 것도 가능함.
  * 쿠키의 제약 
    * 쿠키를 보낼 곳을 제어, 쿠키의 수명을 설정하는 등의 쿠키를 제한하는 속성이 있음.
    * Expires, Max-Age : 쿠키의 수명을 설정
    * Domain : 클라이언트에서 쿠키를 전송할 서버 설정. 쿠키의 스코프를 결정
    * Path : 클라이언트에서 쿠키를 전송할 대상 서버의 경로. Domain과 마찬가지로 쿠키의 스코프를 결정.
    * Secure : https 프로토콜을 사용한 보안 접속일 때만 클라이언트에서 서버로 쿠키를 전송한다.
    * HttpOnly : 크로스 사이트 스크립팅(XSS)공격을 방지하기 위해 사용. 자바스크립트에서 Document.cookie API에 접근할 수 없음.
  * 