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

우리는 네트워크 계층이 혼잡제어를 목적으로 트랜스포트 계층에게 어떤 직접적인 도움을 제공하는지에 따라 혼잡제어 접근을 구별할 수 있다.

<br>

+ ```종단간의 혼잡제어```
  + 혼잡제어에 대한 종단간의 접근법에서 네트워크 계층은 혼잡제어 목적을 위해 트랜스포트 계층에게 어떤 직접적인 지원도 제공하지 않는다.
  + 네트워크에서 혼잡의 존재는 단지 관찰된 네트워크 행동에 기초하여 종단 시스템이 추측해야 한다. (예: 패킷 손실 및 지연)
  + **IP 계층이 네트워크 혼잡에 관해서 종단 시스템에게 어떠한 피드백도 제공하지 않으므로 TCP가 혼잡제어를 위한 종단간의 접근을 수행해야 한다.**
  + 타임아웃 또는 3중의 중복 확인에 의해 나타날 때, TCP 세그먼트 손실은 네트워크 혼잡의 발생으로 생각할 수 있으며 그에 따라 TCP는 윈도우 크기를 줄인다.
  + TCP에 대한 새로운 제안으로 증가하는 RTT를 네트워크 혼잡 증가를 나타내는 것으로 사용하는 것이다.

<br>

+ ```네트워크 지원 혼잡제어```
  + 여기서 네트워크 계층 구성요소는 네트워크 안에서 혼잡상태와 관련하여 송신자에게 직접적인 피드백을 제공한다.
  + 이 피드백은 링크의 혼잡을 나타내는 하나의 비트처럼 간단하다.
  + 예를 들면, XCP 프로토콜은 라우터가 계산하여 피드백을 제공하는데, 라우터가 각각의 출발지에게 처리하는 패킷의 패킷 헤더 안에 어떻게 출발지의 전송률을 증가시키거나 감소시킬 것인지에 관한 정보를 넣어 보내는 것이다.

<br>

```네트워크 지원 혼잡제어```에 대한 혼잡 정보는 전형적인 두 가지 방법 중 하나로 네트워크에서 송신자에게 피드백된다.

+ 직접 피드백
  + 직접 피드백은 네트워크 라우터에서 송신자에게 보내는 것이다.
  + 이 알림의 형태는 전형적으로 초크 패킷(choke packet)의 형태를 갖는다. 
  + 즉, "나는 혼잡하다!"라고 말하는 것이다.

+ 수신자를 경유하는 네트워크 피드백
  + 라우터가 혼잡을 나타내기 위해 송신자에서 수신자에게 흐르는 패킷 안의 특정 필드에 표시/수정하여 표시한다.
  + 이 표시된 패킷을 수신했을 때, 수신자는 혼잡 상태를 송신자에게 알린다.
  + 이 방법은 완전한 왕복시간이 걸린다는 점을 유의해야 한다.

<br><br>
<hr style="border: 2px solid;">
<br><br>

# TCP 혼잡제어
<hr style="border-top: 1px solid;"><br>

위에서 설명했듯이 IP 계층이 네트워크 혼잡에 관해서 종단 시스템에게 어떠한 직접적인 피드백을 제공하지 않으므로, TCP는 ```네트워크 지원 혼잡제어```보다는 ```종단간의 혼잡제어```를 사용해야 한다.

<br>

TCP가 취한 접근방법은 네트워크 혼잡에 따라 연결에 트래픽을 보내는 전송률을 각 송신자가 제한하도록 하는 것이다.

TCP 송신자가 혼잡을 감지하면 송신률을 줄이고, 없음을 감지하면 송신률을 높인다.

단, 이 방법은 세 가지 의문을 제기하는데, ```1) TCP 송신자는 자신의 연결에 송신자 전송 트래픽 전송률을 어떻게 제한하는가?```, ```2) TCP 송신자는 자신과 목적지 사이 경로의 혼잡을 어떻게 감지하는가?```, ```3) 송신자는 종단간의 혼잡을 감지함에 따라 송신율을 변화시키기 위해서 어떤 알고리즘을 사용해야 하는가?```이다.

<br>

먼저 ```TCP 송신자는 자신의 연결에 송신자 전송 트래픽 전송률을 어떻게 제한하는가?```를 본다.

앞에서 TCP 연결의 양 끝 각 호스트들은 수신 버퍼, 송신 버퍼 그리고 몇 가지 변수를 설정하는 것을 보았다.

송신 측에서 동작하는 TCP 혼잡제어 메커니즘은 추가적인 변수인 혼잡 윈도우(congestion window, cwnd)를 기록한다.

cwnd는 TCP 송신자가 네트워크로 트래픽을 전송할 수 있는 비율을 제한하도록 한다. 

특히 송신하는 쪽에서 확인응답이 안된 데이터의 양은 cwnd와 rwnd의 최솟값을 초과하지 않는다.
: ```LastByteSent - LastByteAcked <= min {cwnd, rwnd}```

<br>

그 다음 ```TCP 송신자는 자신과 목적지 사이 경로의 혼잡을 어떻게 감지하는가?```이다.

타임아웃(TCP Tahoe) 또는 수신자로부터 3개의 중복 ACK(TCP Reno)들의 수신 이벤트가 발생했을 때, TCP 송신자 측에 "손실 이벤트(loss event)"가 발생했다고 정의한다.

과도한 혼잡이 발생하면, 경로에 있는 하나 이상의 라우터 버퍼들이 오버플로되고, 그 결과 데이터그램이 버려진다.

버려진 데이터그램은 송신 측에서 손실 이벤트를 발생시키고, 송신자는 송신자와 수신자 사이의 경로상의 혼잡이 발생했음을 알게 된다.

<br>




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
