---
title : 메모리 구조와 함수 호출 규약
categories : [Hacking, System]
tags : [Reversing, 메모리 구조]
---

## 메모리 구조
<hr style="border-top: 1px solid;">

컴파일된 프로그램 메모리는 5개의 세그먼트로 나뉘어짐.

+ 텍스트<sub>text</sub>

+ 데이터<sub>data</sub>

+ bss<sub>block staretd symbol</sub>

+ 힙<sub>heap</sub>

+ 스택<sub>stack</sub>

각 세그먼트는 특정 목적을 위해 존재하는 메모리의 특수 부분을 나타냄.

![image](https://user-images.githubusercontent.com/52172169/150964745-39235646-c6c0-4c64-b2ea-174be524bf44.png)

<br>
<br>
<hr style="border: 2px solid;">
<br>
<br>

### Code 영역
<hr style="border-top: 1px solid;">

실행되는 프로그램의 코드 부분이 저장되는 영역 (변수는 저장하지 않음) , Text 영역이라고도 불림

이 부분에 저장된 내용을 하나씩 처리하며 프로그램이 실행됨

**코드만 저장하고 있으므로 쓰기가 금지되어 있음.**

<br>
<br>

### Data 영역
<hr style="border-top: 1px solid;">

전역변수, 정적 변수 등이 저장되는 공간

프로그램 실행 시 프로그래머가 선언한 변수에 대한 메모리 공간이 할당되고 프로그램 종료 시 해제.

초기화 되지 않은 변수는 BSS영역에 할당됨.

<br>
<br>

### Stack 영역
<hr style="border-top: 1px solid;">
지역 변수와 함수 호출 시 매개 변수가 저장되는 공간

함수 안에서 변수를 선언할 경우 stack에 쌓이게 되고 함수가 종료되면 소멸됨.

Stack 영역은 다른 영역과 달리 위에서 아래로 쌓이는 구조로 되어있음
(높은 주소 -> 낮은 주소)

<br>
<br>

### Heap 영역
<hr style="border-top: 1px solid;">

프로그래머가 동적 할당을 해 생성한 변수가 Heap 영역에 저장됨.

<br>
<br>
<hr style="border: 2px solid;">
<br>
<br>

## 스택의 이해
<hr style="border-top: 1px solid;">

![image](https://user-images.githubusercontent.com/52172169/150964767-61a5506f-c2dc-48b0-b134-3f3684441770.png)

<br>


+ 프로그램 정보 -> 공유 라이브러리 등

+ .text -> 기계어 코드

+ .data -> 전역변수 중 초기화된 데이터

+ .got -> Global Offset Table

+ .bss -> 전역변수 중 초기화되지 않은 데이터

+ heap -> 동적 메모리 영역

+ stack -> 함수관련 정보 : 지역변수, 매개 변수, 리턴주소

+ 프로그램 정보 -> 환경변수, 기타

<br>

스택의 구조는 LIFO(Last-In-First-Out)

```
높은 주소
            ...
            Variable
            SFP (Stack Frame Pointer)
            RET (Return Address) 
            ...
낮은 주소
```

<br>

+ SFP, RET는 함수가 호출되면 기본적으로 스택에 쌓이는 값들임. 

    + SFP에는 이전 ebp의 값이 저장이 됨.

    + RET에는 다음에 실행되어야 할 코드의 주소값이 들어있음.

<br>

예를 들어, main함수는 ```__libc_start_main```에서 호출되어서 RET에는 ```__libc_start_main```의 다음 실행할 코드의 주소가 들어있음. 

```c
int main()
{
	int a = 10;	
	int b = 20;	
	printf("&a = %p, &b = %p", &a, &b); 
  
  // &a = 0xbffffa14, &b = 0xbffffa10 -> a가 더 높은 주소, b가 더 낮은 주소
}
```

<br>
<br>
<hr style="border: 2px solid;">
<br>
<br>

## Calling Convention
<hr style="border-top: 1px solid;">

함수를 호출하는 규약으로 스택을 이용하여 파라미터를 전달할 때 인자 전달 방법, 인자 전달 순서, 
전달된 파라미터가 해제되는 곳, 리턴 값 전달 등을 명시함.

64bit - fastcall 호출규약 / 32bit - cdecl & stdcall & fastcall 모두 사용함.

<br>
<br>

### _cdecl
<hr style="border-top: 1px solid;">

매개 변수 전달 방식 : 우측 -> 좌측

C, C++에서의 default

함수를 호출한 곳에서 파라미터 해제를 담당.

<br>
<br>

### _stdcall
<hr style="border-top: 1px solid;">

매개 변수 전달 방식 : 우측 -> 좌측

함수 내부에서 파라미터 해제를 담당(프로시저 복귀 전 파라미터 해제)


<br>
<br>

### _fastcall
<hr style="border-top: 1px solid;">

매개 변수 전달 방식 : ecx, edx, 우측 -> 좌측(처음 두 개의 파라미터는 ecx, edx에 저장)

함수 내부에서 파라미터 해제를 담당(프로시저 복귀 전 파라미터 해제)

<br>
<br>

### thiscall
<hr style="border-top: 1px solid;">

매개 변수 전달 방식 : ecx, 우측 -> 좌측(처음 한 개의 파라미터는 ecx에 저장)

함수 내부에서 파라미터 해제를 담당(프로시저 복귀 전 파라미터 해제)

<br>
<br>
<hr style="border: 2px solid;">
<br>
<br>

## 추가 자료
<hr style="border-top: 1px solid;">

메모리 구조 : <a href="https://dongdd.tistory.com/36" target="_blank">https://dongdd.tistory.com/36</a>  

기초 지식 : <a href="https://dongdd.tistory.com/79?category=779916" target="_blank">https://dongdd.tistory.com/79?category=779916</a>   





