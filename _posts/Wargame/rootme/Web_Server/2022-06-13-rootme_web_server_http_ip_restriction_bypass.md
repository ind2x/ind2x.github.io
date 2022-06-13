---
title : Root-me IP restriction bypass
categories : [Wargame, Root-me]
tags : [X-Forwarded-For]
---

## HTTP - IP restriction bypass
<hr style="border-top: 1px solid;"><br>

```
Author
Cyrhades,  23 March 2021

Statement
Dear colleagues,

We’re now managing connections to the intranet using private IP addresses, 
so it’s no longer necessary to login with a username / password 
when you are already connected to the internal company network.

Regards,

The network admin
```

<br><br>
<hr style="border: 2px solid;">
<br><br>

## Solution
<hr style="border-top: 1px solid;"><br>

문제에서 내부망에 속해있으면 로그인이 필요 없다고 한다.

따라서 내 IP를 내부망 대역 IP로 변경해줘야 한다.

RFC1918에 따르면 내부망 IP 대역은 아래와 같다.
: ```10.0.0.0        -   10.255.255.255  (10/8 prefix)```
: ```172.16.0.0      -   172.31.255.255  (172.16/12 prefix)```
: ```192.168.0.0     -   192.168.255.255 (192.168/16 prefix)```

<br>


<br><br>
<hr style="border: 2px solid;">
<br><br>
