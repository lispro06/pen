### Let's Encrypt

SSL 은 필수 적용 프로토콜이 되었습니다.

인터넷 웹브라우저에서 https 프로토콜을 사용하지 않거나, 인증서와 도메인이 일치하지 않으면, 경고로 귀찮게 합니다.

유료라는 문제 때문에 적용을 미루는 운영자들이 있어 무료로도 해주고, 쉽게 적용할 수 있는 스크립트들이 배포되고 있습니다.

git clone https://github.com/letsencrypt/letsencrypt

letsencrypt를 로컬 서버에 다운로드 합니다.

./letsencrypt-auto --apache 또는 ./letsencrypt-auto certonly --manual 를 이용해 알맞은 도메인에 적용합니다.

hostname 에 운영하고 있는 도메인을 적용하면 좋을 것 같습니다.

더 친절한 설명들은 인터넷에서 검색을 통해 확인 할 수 있습니다.


### 만난 에러들

fork failed: Cannot allocate memory 를 이유로 sensible-utils 같은 pkg 가 설치되지 않으면, 메모리를 확보하기 위해 사용량이 높은 프로세스를 종료시켜야 합니다.

top, kill, dpkg -i *.deb

www와 www를 쓰지 않는 이슈로 멀티도메인 적용 문제가 있는데, --manual 옵션으로 www x-www second x-second 콤마 또는 띄어쓰기를 이용해 등록하고,

./letsencrypt-auto 를 한번 더 실행시키거나 apache를 재실행 시키면 적용됩니다.

hostname에 설정된 도메인이 메인으로 되고, 서브 도메인이나 추가 도메인은 드러나지 않는 듯 합니다.

3개월동안은 잘 안되었는데, 자동 스크립트가 개선되어 그런 것으로 추측됩니다.


### 윈도우는....

윈도우의 IIS에는 https://github.com/Lone-Coder/letsencrypt-win-simple/releases 로 소개되었었는데, https://github.com/PKISharp/win-acme/releases 로

이동되는 것으로 보아 업데이트 하면서 개선되어 수정된 것을 생각됩니다.

IIS 도 어렵지 않게 자동 스크립트의 이용이 가능합니다.


### http -> https ?

권장되는 웹서버 운영은 http로 접근할 경우 https 로 전환시켜는 것입니다.

하지만, 여러 포트를 운영하거나, http 를 이용한 서비스를 별도 운영, 부득이하게 http로 접근하도록 허용해야할 경우 옵션을 사용하지 않을 수도 있습니다.

letsencrypt 자동 스크립트에서는 http -> https 적용에 대한 옵션을 제공하므로 영향이 염려될 경우 N 을 선택하면 됩니다.


### openssl 취약점

openssl 취약점은 지속적으로 발견될 전망입니다. 기술이 발전하면서 과거 기술에 대한 취약점은 약점에서 취약점으로 증명되는 과정을 겪고 있습니다.

$ openssl version

OpenSSL 1.0.2g  1 Mar 2016

이 서버의 openssl 버전은 1.0.2g 로 몇 개월은 버틸 수 있을 것 같습니다. 영향이 경미하겠지만,

heartbleed나 더 엄청난 취약점들이 기다리고 있으니, 항상 패치를 준비해야 하겠습니다.
