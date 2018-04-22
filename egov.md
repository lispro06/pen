### 전자정부 표준프레임워크

iBatis SQL Maps;MyBatis 과 스프링 기반의 java 기반의 정보시스템 구축에 활용하실 수 있는 개발·운영 표준 환경을 제공하기 위한 것입니다.

공공기관의 요구조건을 충족하기 때문에 검수에 대한 부담을 줄일 수 있고, 최근 보안 기능도 많이 적용되어 신뢰할만 합니다.

### HTMLTagFilterRequestWrapper.java

3.7.0의 경우 getParameterValues, getParameter 메소드에 대해 XSS 공격 방어가 적용되어 있습니다.

<pre><code>
switch (c) {
	case '<':
		strBuff.append("＆lt;");
		break;
	case '>':
		strBuff.append("＆gt;");
		break;
	case '&':
		strBuff.append("＆amp;");
		break;
	case '"':
		strBuff.append("＆quot;");
		break;
	case '\'':
		strBuff.append("＆apos;");
		break;
	default:
		strBuff.append(c);
		break;
}
</code></pre>

### HTMLTagFilter.java

doFilter 메소드에 HTMLTagFilterRequestWrapper 클래스를 적용하여, HttpServletRequest에 의한 입력 값 필터링을 수행한다.

web.xml 에 처리되는 확장자와 필터 클래스가 정의되어 있으니, 해당 파일을 먼저 확인하여 경로를 찾아보면 도움이 된다.

<pre><code>

 &lt;filter>
		&lt;filter-name>HTMLTagFilter&lt;/filter-name>
		&lt;filter-class>egovframework.rte.ptl.mvc.filter.HTMLTagFilter&lt;/filter-class>
	&lt;/filter>
	&lt;filter-mapping>
		&lt;filter-name>HTMLTagFilter&lt;/filter-name>
		&lt;url-pattern>*.do&lt;/url-pattern>
	&lt;/filter-mapping>

</code></pre>
	
### iBatis SQL Maps

동적 바인딩이 아닌 정적 바인딩을 사용하여 SQL Injection 에 대한 위협이 낮습니다.

<pre><code>
	&lt;select id="selectSampleList" parameterType="searchVO" resultType="egovMap">
			SELECT
				ID, NAME, DESCRIPTION, USE_YN, REG_USER
			FROM SAMPLE
			WHERE 1=1
			&lt;if test="searchKeyword != null and searchKeyword != ''">
		        &lt;choose>
		            &lt;when test="searchCondition == 0">
						AND	ID LIKE '%' || #{searchKeyword} || '%'
					&lt;/when>
		            &lt;when test="searchCondition == 1">
						AND	NAME LIKE '%' || #{searchKeyword} || '%'
					&lt;/when>
				&lt;/choose>
			&lt;/if>
			ORDER BY ID ASC
			LIMIT #{recordCountPerPage} OFFSET #{firstIndex}
	&lt;/select>
</code></pre>

### EgovSampleController.java

lab101-project-create-tutor 의 주요 파일로 데이터 리스팅, 입력, 삭제 관련 매소드를 정의하고 있습니다.

입력 파라미터 중 UseYn은 char(1) 로 선언되어 2자리 이상이되면 오류라 발생합니다.
 
&나 '가 필터 메소드에 의해 변환되더라도 "&"가 붙으므로 이를 제거해 줄 필요가 있습니다.

<pre><code>
sampleVO.setUseYn(sampleVO.getUseYn().replaceAll("&", "").substring(0, 1));
</code></pre>

Y나 N만 들어가게 하려면 조건문이 하나 더 필요한데, 입력 값이 원하는 것이 아닐 경우 기본 N으로 처리하도록 하는 코드는 아래와 같습니다.

<pre><code>
if(sampleVO.getUseYn() != "Y"){
	if(sampleVO.getUseYn() != "N"){
		sampleVO.setUseYn("N");
	}
}
</code></pre>

### server.xml

기존에 사용하는 프록시도구나 WAS가 있어 8080 포트를 사용 중이라면, 설정 파일에서 포트를 변경하여 사용 가능합니다.

<pre><code>
&lt;Connector connectionTimeout="20000" port="8090" protocol="HTTP/1.1" redirectPort="8443"/>
</code></pre>
