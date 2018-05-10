### Postman

Postman은 HTTP Request, Response 패킷을 통하여 개발한 API서버를 용이하게 테스트 할 수 있는 툴입니다.
Fiddler나 Burpsuit에서도 패킷을 보내거나 받을 수 있지만 Postman은 프록시 설정을 하지 않아도 된다는 장점을 가지고 있으며,
API서버 테스트에 용이하도록 GUI 환경이 구성되어있습니다.

### 설치하기

Postman은 크롬 브라우저의 확장 프로그램으로 구글에서 설치할 수 있습니다.

초기화면

<div>
<img src="https://github.com/boanit/pen/blob/master/installation.PNG" width="90%"></img>
</div>

### <c: out> 적용하기
<pre><code><%
 String securecoding = "hello, boanit!";
 request.setAttribute("securecoding", securecoding);
%>

escapeXml false
< c:out escapeXml="false" value="${securecoding}" />
escapeXml true
< c:out escapeXml="true" value="${securecoding}" />
default
< c:out value="${securecoding}" />
</code></pre>
* escapeXml은 생략될 경우 default로 true가 설정됩니다.


### fn:escapeXml()함수 라이브러리 설치하기

먼저  jstl 사용을 위하여 http://tomcat.apache.org/taglibs/standard/ 에서 jstl 1.1 버전을 설치합니다.

설치 후 lib 디렉토리에서 jstl.jar, standard.jar 파일을 WEB-INF/lib 디렉토리로 복사합니다.

필터를 적용할 jsp파일에서 jstl function 사용을 위한 선언을 합니다.
<pre><code><%@ taglib uri="http://java.sun.com/jsp/jstl/functions" prefix="fn" %>
</code></pre>

### fn:escapeXml() 적용하기
<pre><code><%
 String securecoding = "hello, boanit!";
 request.setAttribute("securecoding", securecoding);
%>

With escapeXml() Function:
<p>string-1 : ${fn:escapeXml(securecoding)}</p>  
Without escapeXml() Function:
<p>string-2 : ${securecoding}</p></code></pre>
