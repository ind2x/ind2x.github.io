---
title : "Transport Layer 2"
categories : [Study, Computer Network]
tags : [Transport Layer]
---

# Transport Layer 1
<hr style="border-top: 1px solid;"><br>

Link 
: <a href="https://ind2x.github.io/posts/Transport_Layer/" target="_blank">ind2x.github.io/posts/Transport_Layer/</a>

<br><br>
<hr style="border: 2px solid;">
<br><br>

# 혼잡제어의 원리
<hr style="border-top: 1px solid;"><br>

네트워크 혼잡 원인을 처리하기 위해서 네트워크 혼잡을 일으키는 송신자를 억제하는 메커니즘이 필요하다.

<br><br>

## 혼잡의 원인과 비용
<hr style="border-top: 1px solid;"><br>

혼잡제어가 발생하는 단계적으로 복잡해지는 세 가지 시나리오들을 살펴본다.

각 경우에서 왜 혼잡이 발생하는지와 그 혼잡비용에 대해 먼저 살펴본다.

<br><br>

### 시나리오 1
<hr style="border-top: 1px solid;"><br>

시나리오1은 **2개의 송신자와 무한 버퍼를 갖는 하나의 라우터**이다.

가장 간단한 혼잡제어 시나리오로 호스트 A,B가 호스트 C,D로 데이터를 전송하는데 경로 상에 A,B와 C,D 사이에는 각각 단일 홉이 있고 그 홉을 연결하는 무한 버퍼를 가진 라우터가 있다고 가정한다.

이 때, 라우터는 용량 R의 출력 링크를 갖는다.

<br>

"연결당 처리량"이라고 있는데 이는 "수신자측에서의 초당 바이트 수"로 살펴보면, 0부터 R/2 까지는 송신자의 전송률과 수신자의 처리량이 같다.

하지만, 전송률이 R/2 이상일 땐, 수신률은 여전히 R/2인데 그 이유는 송신자가 2명인데 용량이 R인 링크는 하나이기 때문이다. 

R/2의 연결당 처리량을 얻는 것은 목적지에 패킷을 전달하는 데 링크를 최대로 활용하므로 좋은 현상이다.

<br>

그러나 전송률이 R/2에 근접할 때 평균 지연이 증가한다.

전송률이 R/2를 초과할 때, 라우터 안에 큐잉된 패킷의 평균 개수는 제한되지 않고, 출발지와 목적지 사이의 평균 지연이 무제한이 된다.

<br>

따라서 R 근처의 전체 처리량에서 동작하는 것은 처리량 관점에서는 이상적이나, 지연 관점에서는 이상적이지 않다.

즉, 이 시나리오의 네트워크 혼잡 비용은 **패킷 도착률이 링크 용량에 근접함에 따라 큐잉 지연이 커진다.**

<br><br>

### 시나리오 2
<hr style="border-top: 1px solid;"><br>



<br><br>

### 시나리오 3
<hr style="border-top: 1px solid;"><br>



<br><br>

## 혼잡제어에 대한 접근법
<hr style="border-top: 1px solid;"><br>



<br><br>
<hr style="border: 2px solid;">
<br><br>

# TCP 혼잡제어
<hr style="border-top: 1px solid;"><br>



<br><br>

## 슬로 스타트
<hr style="border-top: 1px solid;"><br>



<br><br>

## 혼잡 회피
<hr style="border-top: 1px solid;"><br>



<br><br>

## 빠른 회복
<hr style="border-top: 1px solid;"><br>



<br><br>

## TCP 혼잡제어: 복습
<hr style="border-top: 1px solid;"><br>



<br><br>

## 공평성
<hr style="border-top: 1px solid;"><br>



<br><br>

## 공평성과 UDP
<hr style="border-top: 1px solid;"><br>



<br><br>

## 공평성과 병령 TCP 연결
<hr style="border-top: 1px solid;"><br>



<br><br>

## 명시적 혼잡 표시
<hr style="border-top: 1px solid;"><br>



<br><br>
<hr style="border: 2px solid;">
<br><br>

# 요약
<hr style="border-top: 1px solid;"><br>



<br><br>
<hr style="border: 2px solid;">
<br><br>

# 참고
<hr style="border-top: 1px solid;"><br>

Link
: <a href="https://justlog.tistory.com/m/8" target="_blank">justlog.tistory.com/m/8 - RDT Protocol</a>
: <a href="https://justlog.tistory.com/m/11" target="_blank">justlog.tistory.com/m/11 - GBN & Selective repeat</a>
: <a href="https://justlog.tistory.com/m/15" target="_blank">justlog.tistory.com/m/15 - TCP</a>
: <a href="https://velog.io/@tonyhan18/series/21-기초컴퓨터네트워크" target="_blank">velog.io/@tonyhan18/series/21-기초컴퓨터네트워크</a>
: <a href="https://www.cnsr.dev/index_files/Classes/Networking/Content/03-Transport.html" target="_blank">cnsr.dev/index_files/Classes/Networking/Content/03-Transport.html</a>

<br><br>
<hr style="border: 2px solid;">
<br><br>
