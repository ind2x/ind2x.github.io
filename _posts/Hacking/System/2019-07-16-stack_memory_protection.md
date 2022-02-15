---
title : Linux Stack Memory Protection and bypass (Incomplete)
categories : [Hacking, System]
tags : [스택 메모리 보호기법, ASLR, NX, SSP, Stack Smashing Protector, Stack Canary, RELRO, PIE, Incomplete]
---

## NX
<hr style="border-top: 1px solid;"><br>

```NX : No -eXecute```

<br>

실행할 코드영역을 제외한 메모리 영역에 실행권한 제거. 

**즉, 스택을 실행 불가능하게 만드는 것이다.**

<br>

+ 해제: (컴파일시) ```gcc ~~ -z execstack```

<br>

+ bypass : 실행권한이 있는 메모리를 이용한 기법 (RTL,ROP,etc ...)

<br>

+ 확인방법 : ```readelf -a [file] | grep STACK``` -> RW가 있으면 적용되어 있는 것

<br><br>
<hr style="border: 2px solid;">
<br><br>

## ASLR
<hr style="border-top: 1px solid;"><br>

```Address Space Layout Randomization (공격자가 쉽게 주소값을 알지 못하게 해주는 보호기법)``

실행마다 스택의 배치가 무작위로 바뀌게 된다.

<br>

+ ```/proc/sys/kernel/randomize_va_space``` :  파일의 값을 확인하면 알 수 있음.
  + 0 : 적용 x
  + 1 : 스택, 힙 메모리 랜덤화
  + 2 : 스택, 힙, 라이브러리 메모리 랜덤화

<br>

+ 스택을 포함한 메모리의 주소를 랜덤하게 할당.

+ 완전한 랜덤은 아님, 순서와 패턴을 어느정도 유지한 채로 랜덤하게 함.

+ 해제: ```(sudo) sysctl -w kernel.randomize_va_space=0(=1,2 는 on, 0은 off)```

+ bypass : nop sledding, leak, etc...


<br><br>
<hr style="border: 2px solid;">
<br><br>

## SSP(Stack Smashing Protector)
<hr style="border-top: 1px solid;"><br>


메모리 커럽션 취약점 중 스택 버퍼 오버플로우 취약점을 막기 위해 개발된 보호 기법.

스택 버퍼와 스택 프레임 포인터 사이에 랜덤 값을 삽입하여 함수 종료 시점에서 랜덤 값 변조 여부 검사

<br>

SSP 보호 기법이 적용되어 있으면 함수에서 스택 사용 시 카나리 생성

마스터 카나리는 main함수 호출 전 랜덤으로 생성된 카나리를 ```TLS(Thread Local Storage)```에 저장

TLS 영역의 ```header.stack_guard```에 카나리 값 삽입 


<br><br>

### Stack Canary
<br>

- 스택의 끝부분에 임의의 값을 넣고 함수 종료 시 이 값이 변조되었으면 스택 오염으로 판단

- 리눅스의 경우 ```gs:0x14``` 값

- 해제 : (컴파일시) ```gcc ~~ -fno-stack-protector```

- bypass : leak? got overwrite?


<br><br>
<hr style="border: 2px solid;">
<br><br>

## RELRO(Relocation Read-Only)
<hr style="border-top: 1px solid;"><br>



<br><br>
<hr style="border: 2px solid;">
<br><br>

## PIE(Position Independent Executable)
<hr style="border-top: 1px solid;"><br>



<br><br>
<hr style="border: 2px solid;">
<br><br>
