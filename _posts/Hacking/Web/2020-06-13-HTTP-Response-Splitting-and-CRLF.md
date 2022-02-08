---
title : HTTP Response Splitting and CRLF (Incompleted)
categories : [Hacking, Web]
tags : [HTTP Response Splitting, Incomplete]
---

## 1. CRLF
```
CR : Carriage Return -> 현재 위치를 나타내는 커서를 맨 앞으로 이동시킨다 -> \r, %0D

LF : Line Feed -> 커서의 위치를 아랫줄로 이동시킨다 -> \n, %0A
```

## 2. HTTP Response Splitting
```
CWE-113

HTTP Request에 있는 파라미터가 HTTP Response의 Header에 그대로 전달되는 경우 파라미터에 
CRLF가 존재하면 HTTP 응답이 분리될 수 있다는 취약점을 이용한 공격. 
Response Header에 악의적인 코드를 주입함으로써 XSS 및 캐시를 훼손할 수 있음.
```
