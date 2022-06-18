---
title : JSON Web Token (JWT) And Attacking JWT Authentication
date: 2022-06-18-13:07 +0900
categories : [Hacking, Web]
tags : [JSON Web Token, JWT Attacking]
---

## Json Web Token
<hr style="border-top: 1px solid;"><br>



<br><br>
<hr style="border: 2px solid;">
<br><br>

## Attacking JWT
<hr style="border-top: 1px solid;"><br>

JWT의 공격 방법에는 4가지가 있다.
: 1. 단순히 JWT를 디코딩을 해주기만 해도 어떤 값이 들어있는지 알 수 있다.
: 2. 취약한 버전의 JWT에서는 알고리즘을 none으로 변경해주면 서버에서 signature에 대한 검증을 하지 않아 signature 없이 인증이 된다.
: 3. HS256 등 대칭 키 암호 알고리즘에 Brute Force 공격을 통해 취약한 키를 흭득
: 4. 


<br><br>
<hr style="border: 2px solid;">
<br><br>
