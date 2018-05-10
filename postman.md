### Postman

Postman은 HTTP Request, Response 패킷을 통하여 개발한 API서버를 용이하게 테스트 할 수 있는 툴입니다.
Fiddler나 Burpsuit에서도 패킷을 보내거나 받을 수 있지만 Postman은 프록시 설정을 하지 않아도 된다는 장점을 가지고 있으며,
API서버 테스트에 용이하도록 GUI 환경이 구성되어있습니다.

### 설치하기

Postman은 크롬 브라우저의 확장 프로그램으로 구글에서 설치할 수 있습니다.

초기화면

<div>
<img src="https://github.com/boanit/pen/blob/master/installation2.PNG" width="90%"></img>
</div>

### 사용하기

먼저 요청하고자하는 URL 및 요청 메소드를 선택합니다.

선택 후 헤더 영역을 요청하고자 하는 API 양식에 맞추어 작성합니다.
(OAuth, AWS Signature 등 API 서버의 인증이 필요할 경우 Authorization 메뉴를 통해 인증 키 혹은 ID/PWD를 설정할 수 있습니다.)

<div>
<img src="https://github.com/boanit/pen/blob/master/test01.PNG" width="90%"></img>
</div>

헤더 영역을 모두 작성한 후 바디 영역을 작성합니다.

<div>
<img src="https://github.com/boanit/pen/blob/master/test02.PNG" width="90%"></img>
</div>


