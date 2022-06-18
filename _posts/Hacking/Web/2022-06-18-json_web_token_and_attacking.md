---
title : JSON Web Token (JWT) And Attacking JWT Authentication
date: 2022-06-18-13:07 +0900
categories : [Hacking, Web]
tags : [JSON Web Token, JWT Attacking]
---

## Json Web Token
<hr style="border-top: 1px solid;"><br>

참고 자료 
: <a href="https://brunch.co.kr/@jinyoungchoi95/1" target="_blank">brunch.co.kr/@jinyoungchoi95/1</a>

<br>



<br><br>
<hr style="border: 2px solid;">
<br><br>

## Attacking JWT
<hr style="border-top: 1px solid;"><br>

JWT의 공격 방법에는 요약하면 4가지가 있다.

+ 단순히 JWT를 디코딩을 해주기만 해도 어떤 값이 들어있는지 알 수 있다.

+ 취약한 버전의 JWT에서는 알고리즘을 none으로 변경해주면 서버에서 signature에 대한 검증을 하지 않아 signature 없이 인증이 된다.

+ HS256 등 대칭 키 암호 알고리즘에 만약 키가 취약한 경우, Brute Force 공격을 통해 키를 흭득할 수 있다.

+ 비대칭 암호 (RS256 등)에서 대칭 암호 (HS256 등)으로 알고리즘을 변경하는 경우, 비대칭 암호에서 사용하는 공개 키가 대칭키의 비밀 키로 사용되어 인증 할 수 있다.

<br>

자세한 공격 방법은 <a href="https://dohunny.tistory.com/m/15" target="_blank">dohunny.tistory.com/m/15</a>과 아래 참고자료에서 확인

## 참고자료
<hr style="border-top: 1px solid;"><br>

Link
: <a href="https://dohunny.tistory.com/m/15" target="_blank">dohunny.tistory.com/m/15</a>  --> GOOD
: <a href="https://www.sjoerdlangkemper.nl/2016/09/28/attacking-jwt-authentication/" target="_blank">sjoerdlangkemper.nl/2016/09/28/attacking-jwt-authentication/</a>
: <a href="https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Hacking%20JSON%20Web%20Token%20(JWT)%20-%20Rudra%20Pratap.pdf" target="_blank">EN - Hacking JSON Web Token (JWT) - Rudra Pratap</a>

<br><br>
<hr style="border: 2px solid;">
<br><br>
