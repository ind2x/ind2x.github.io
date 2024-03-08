---
title: Buffer Overflow 몰랐던 내용
categories: [Hacking, System]
tags: [Linux, BOF, 메모리 주소 체계, 환경 변수]
---

## x86, x64 메모리 주소 체계 (BOF)
<hr style="border-top: 1px solid;"><br>

32/64비트 메모리 주소 체계
: <a href="https://hackstoryadmin.tistory.com/78?category=276534" target="_blank">hackstoryadmin.tistory.com/78?category=276534</a>

<br>

스택과 레지스터를 32비트는 4바이트씩 구분하고, 64비트는 8바이트씩 구분을 한다.

여기서 중요한점은 64비트에서는 8바이트로 구분은 하지만 앞의 2바이트는 사용하지 않는다고 함.

즉, 실질적으로 6바이트만 사용하고 앞의 2바이트는 0x0000이 되는 것.

BOF할 때, 64비트 프로그램에 대해서는 주의해야 함.
: <a href="https://hackstoryadmin.tistory.com/entry/x64-BOFBuffer-Overflow" target="_blank">hackstoryadmin.tistory.com/entry/x64-BOFBuffer-Overflow</a>

<br><br>
<hr style="border: 2px solid;">
<br><br>

## 쉘코드 삽입 시 파이썬 버전에 따른 차이
<hr style="border-top: 1px solid;">

쉘코드를 삽입을 했는데 hex 값이 변하는 경우가 있음. 

이 경우는 python3의 변환방식 때문에 발생하는 문제임.
: <a href="https://security.stackexchange.com/questions/270884/bufferoverflow-chars-gets-replaced-on-stack" target="_blank">security.stackexchange.com/questions/270884/bufferoverflow-chars-gets-replaced-on-stack</a>

<br>

예를 들어, ```\x90```을 python3을 이용해 전달한다면 이 값이 ```\xc2```로 변하였음.

또는 ```\xff```가 ```\xbf\xc3```으로 변하기도 함.

<br>

```shell
r `python3 -c 'print("\x90"*88+"AABBCC")'`

gdb-peda$ x/gx $rbp-0x50
0x7fffffffe310: 0x90c290c290c290c2
```

<br>

```shell
r `python3 -c 'print("\xff"*88+"AABBCC")'`

gdb-peda$ x/gx $rbp-0x50
0x7fffffffe310: 0xbfc3bfc3bfc3bfc3
```

<br>

그래서 웬만하면 파이썬2로 하면 좋겠지만 없다면 perl을 이용해서 하던가, python3 뿐이라면 이 방법은 나중에 찾아보기

<br><br>
<hr style="border: 2px solid;">
<br><br>

## gdb와 실제 바이너리 차이
<hr style="border-top: 1px solid;">

gdb에서는 내가 작성한 payload가 잘 작동해서 쉘이 흭득되는데, 바이너리에서는 segmentation fault가 뜨는 경우
: <a href="https://reverseengineering.stackexchange.com/questions/16677/why-does-my-shellcode-work-in-gdb-but-not-on-the-command-line" target="_blank">reverseengineering.stackexchange.com/questions/16677/why-does-my-shellcode-work-in-gdb-but-not-on-the-command-line</a>

<br>

리눅스 환경변수에 터미널 사이즈와 관련된 변수인 ```$LINES```와 ```$COLUMNS```가 있음.

이 두 값이 gdb 실행 시 영향을 주나봄. 그래서 메모리 주소들에 영향을 줘서 gdb에서 먹힌 ret 주소가 실제 바이너리에서는 안되는 것임.

그래서 gdb 실행 후 ```unset env LINES```와 ```unset env COLUMNS```를 해준 후 확인한 ret 주소를 이용하면 실제 바이너리에서도 동일하게 동작하게 됨.

<br><br>
<hr style="border: 2px solid;">
<br><br>

## setuid와 setreuid 쉘코드 차이점
<hr style="border-top: 1px solid;">

쉘코드 만드는 과정
: <a href="https://hdacker.tistory.com/20" target="_blank">hdacker.tistory.com/20</a>

<br>

setreuid 부분 내용
: <a href="https://hdacker.tistory.com/21" target="_blank">hdacker.tistory.com/21</a>

<br>

정리하면, setuid는 

<br><br>
<hr style="border: 2px solid;">
<br><br>

## 쉘코드 모음
<hr style="border-top: 1px solid;">

shellcode
: <a href="https://shell-storm.org/shellcode/index.html" target="_blank">shell-storm.org/shellcode/index.html</a>

<br><br>
<hr style="border: 2px solid;">
<br><br>
