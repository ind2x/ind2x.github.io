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

![image](https://user-images.githubusercontent.com/52172169/178232000-824f15a8-7e81-4fcc-b49c-89beb339ae11.png)

<br>

시나리오1은 **2개의 송신자와 무한 버퍼를 갖는 하나의 라우터**이다.

가장 간단한 혼잡제어 시나리오로 호스트 A,B가 호스트 C,D로 데이터를 전송하는데 경로 상에 A,B와 C,D 사이에는 각각 단일 홉이 있고 그 홉을 연결하는 무한 버퍼를 가진 라우터가 있으며 신뢰적 연결이 아닌 단순히 데이터를 캡슐화해서 전송하기만 한다고 가정한다.

이 때, 라우터는 용량 R의 출력 링크를 갖는다.

<br>

![image](https://user-images.githubusercontent.com/52172169/178232064-1c4f515b-15dd-4583-8b13-c8c7ac40815a.png)

<br>

왼쪽 그래프는 "연결당 처리량"이라고 있는데 이는 "수신자측에서의 초당 바이트 수"로 살펴보면, 0부터 R/2 까지는 송신자의 전송률과 수신자의 처리량이 같다.

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

![image](https://user-images.githubusercontent.com/52172169/178232171-0cc66b16-5071-435e-95d5-b0472919ac5d.png)

<br>

시나리오2는 1에서 라우터의 버퍼가 유한하고, 신뢰적인 연결이라 가정한다.

시나리오2에서의 성능은 재전송이 어떻게 수행되는지에 따른다.

<br>

먼저 비현실적인 경우로 라우터에 있는 버퍼가 비어있을 때만 패킷을 송신한다는 가정이다.

처리율 관점에서 보면, 송신된 모든 것이 수신되기 때문에 성능은 이상적이며, 패킷 손실이 절대로 발생하지 않으므로 송신율은 R/2를 초과할 수 없다.

또한 R/2까지의 송신율과 수신자의 처리율은 동일하다.

<br>

두 번째는 패킷이 확실히 손실된 것을 알았을 때만, 송신자가 재전송하는 좀 더 현실적인 경우다.

최초의 데이터 전송과 재전송합의 속도가 R/2라 가정하면, 이 값에서 수신자 애플리케이션으로 전달되는 데이터의 전송률은 R/3이다.

그러므로 전송된 데이터의 R/2 중 0.333R 바이트는 원래의 데이터고, 초당 0.166R 바이트는 재전송 데이터이다.

여기서 혼잡 네트워크 비용은 송신자는 버퍼 오버플로 때문에 버려진 패킷을 보상하기 위해 재전송을 수행해야 한다.

<br>

마지막으로 송신자에서 너무 일찍 타임아웃 되어 패킷이 손실되지 않았으나 큐에서 지연 중인 패킷을 재전송한 경우다.

이 경우 원래의 데이터 패킷과 재전송 패킷 둘 다 수신자에게 도착한다.

물론 수신자는 하나의 패킷만 필요하므로 재전송된 패킷은 버린다.

여기서 발생하는 혼잡 비용은 커다란 지연으로 인한 송신자의 불필요한 재전송은 라우터가 패킷의 불필요한 복사본들을 전송하는데 링크 대역폭을 사용하는 원인이 된다.

<br><br>

### 시나리오 3
<hr style="border-top: 1px solid;"><br>

![image](https://user-images.githubusercontent.com/52172169/178232583-4f104068-c4d9-404c-9c48-01b4effd4375.png)

<br>

시나리오3은 4개의 송신자와 유한 버퍼를 가지는 라우터, 그리고 멀티홉 경로이다.

예를 들면, B-C 사이의 라우터를 R2라고 할 때, R2에 도착하는 B-D 트래픽이 A-C 트래픽 보다 클 수 있다.

A-C와 B-D 트래픽은 R2에서 버퍼공간을 경쟁해야 하므로, R2를 성공적으로 통과하는 A-C 트래픽 양은 B-D에서 제공된 부하가 크면 클수록 더 작아진다.

극단적인 경우, 제공된 부하가 무한대에 가까워 짐에 따라, R2의 빈 버퍼는 즉시 B-D의 패킷으로 채워지고, R2에서의 A-C 연결의 처리량은 0이 된다.

즉, 트래픽이 많은 경우 A-C 종단간 처리율이 0이 된다는 것으로 제공된 부하와 처리량 간의 tradeoff가 발생함을 보여준다.

![image](https://user-images.githubusercontent.com/52172169/178249294-dbe9a43c-89f2-4e39-a31d-1e32a47cc3ee.png)

<br>

서로 같은 경로를 지나는 순간이 존재하면 서로의 영향을 받게 되며, 너무 많은 패킷을 보내려다가 둘 다 못보낼 수도 있다.

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
