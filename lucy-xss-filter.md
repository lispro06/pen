### lucy-xss-filter

Lucy-XSS는 네이버에서 제공하는 XSS 방어를 위한 오픈 소스 라이브러리이며, 

블랙리스트 방식이 아닌 화이트리스트 방식의 필터가 적용되어 보다 강력할 보안을 적용할 수 있습니다.

아래에선 lucy-xss-filter 설치 및 적용 방법을 다루겠습니다.

### 설치 하기

https://github.com/naver/lucy-xss-filter 에서 아래의 파일을 설치합니다.

- lucy-xss-1.6.2.jar    Lucy-XSS Filter 라이브러리 파일

- lucy-xss-superset.xml 화이트 리스트 기본 보안 설정 파일

- lucy-xss.xml          화이트 리스트 사용자 설정 파일

### 설정 하기

lucy-xss-filter에는 아래와 같이 3가지 화이트 리스트 설정 파일이 있으며

사용 환경 및 서비스 특성에 맞는 설정 파일을 선택해서 사용할 수 있습니다.

1. lucy-xss-default.xml은 jar파일에 포함되어 배포되는 Lucy-XSS Filter의 
   기본 설정 파일로 html element와 attribute가 선언되어있습니다.

2. lucy-xss-superset.xml은 lucy-xss-default.xml을 상속받아 작성된 파일이며 
   최신 보안 설정이 추가되어 있습니다.

3. lucy-xss.xml은 사용자가 작성하는 xml파일로 서비스 특성에 맞게 필터링을 적용할 수 있습니다.

* Filter 인스턴스를 생성할 때 설정 파일명을 지정하지 않으면 디폴트로 lucy-xss.xml파일을 읽어서 사용합니다.

사용 환경 특성에 맞는 화이트 리스트 파일을 선택하여 아래의 경로에 설치합니다. 

lucy-xss-1.6.2.jar 파일은 /WEB-INF/lib 경로에 복사합니다.

화이트 리스트 설정 파일은 /src 경로에 복사합니다.

### lucy-xss-superset.xml
<pre><code> <?xml version="1.0" encoding="UTF-8"?>
	<elementRule>
		<element name="body" disable="true" />
		<element name="embed" disable="true" />
		<element name="iframe" disable="true" />
		<element name="meta" disable="true" />
		<element name="object" disable="true" />
		<element name="script" disable="true" />
		<element name="style" disable="true" />
	</elementRule>
	
	<attributeRule>
		<attribute name="data" base64Decoding="true">
			<notAllowedPattern><![CDATA[(?i:s\\*c\\*r\\*i\\*p\\*t)]]></notAllowedPattern>
			<notAllowedPattern><![CDATA[&[#\\%x]+[\da-fA-F][\da-fA-F]+]]></notAllowedPattern>
		</attribute>
		<attribute name="src" base64Decoding="true">
			<notAllowedPattern><![CDATA[(?i:s\\*c\\*r\\*i\\*p\\*t)]]></notAllowedPattern>
			<notAllowedPattern><![CDATA[&[#\\%x]+[\da-fA-F][\da-fA-F]+]]></notAllowedPattern>
		</attribute>
		<attribute name="style">
			<notAllowedPattern><![CDATA[(?i:e\\*x\\*p\\*r\\*e\\*s\\*s\\*i\\*o\\*n)]]></notAllowedPattern>
			<notAllowedPattern><![CDATA[&[#\\%x]+[\da-fA-F][\da-fA-F]+]]></notAllowedPattern>
		</attribute>
	</attributeRule>

</code></pre>

### 적용하기

출력 값이 생성되는 파일에 filter를 적용합니다.

<pre><code>
import com.nhncorp.lucy.security.xss.XssFilter;
		String data=request.getParameter("data");
				out.println(data);
		XssFilter filter = XssFilter.getInstance("lucy-xss-superset.xml");
		String FilteredData filter.doFilter(data); 
		out.println(FilteredData);
		</code></pre>

		


