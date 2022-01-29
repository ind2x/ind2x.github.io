---
title: 환경변수 설정 및 주소 구하기
categories: [Hacking, System]
tags: [Linux, BOF, 환경변수]
---

## 1. 환경변수 설정 및 해제
1회성 설정 방법
```
env : 환경변수 조회 및 해제
env NAME=VALUE : NAME 환경변수에 VALUE 값 지정
env -u NAME : NAME 환경변수 제거
```
```
set NAME=VALUE : NAME 환경변수에 VALUE 값 지정, bash 에선 set 생략 가능
unset NAME : NAME 환경변수 해제
```
```
export NAME=VALUE 
```
영구 설정 방법은 참고자료에서 확인

<br>
<br>

## 2. 환경변수 주소 구하기
```c
#include <stdio.h>
#include <unistd.h>

int main(int argc, char *argv[])
{
   printf("env : %p\n", getenv(argv[1]));
   return 0;
}
```

환경 변수에서 중요한 부분은 **환경 변수가 스택에 위치한다는 점**과 셸에서 값을 설정할 수 있다는 점이다.

환경변수의 주소를 구할 때, 프로그램 이름의 길이가 환경변수 위치에 영향을 준다. 

만약, 프로그램 이름 길이가 한 바이트 늘어나면 환경 변수 주소는 두 바이트 줄어든다.



<br>
<br>

## Reference
<hr style="border-top: 1px solid;">

<a href="https://sites.google.com/site/sunitwarehouse/os/linux/0001" target="_blank">https://sites.google.com/site/sunitwarehouse/os/linux/0001</a>  
<a href="https://hashcode.co.kr/questions/1893/%EB%A6%AC%EB%88%85%EC%8A%A4-%ED%99%98%EA%B2%BD%EB%B3%80%EC%88%98-%EC%84%A4%EC%A0%95%ED%95%A0-%EB%95%8C-env-set-export-declare" target="_blank">set, env, export, declare 차이점</a>  

