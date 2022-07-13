---
title: Network Layer Data Plane
date: 2022-07-13-12:24  +0900
categories: [Study, Computer Network]
tags: [Network Layer]
---

# 네트워크 계층 개요
<hr style="border-top: 1px solid;"><br>

![네트워크 계층](https://user-images.githubusercontent.com/52172169/178651428-21b49494-6ddc-4130-895d-653db3e3d3b5.png)

<br>

위의 그림은 H1과 H2의 경로상에 여러 라우터와 두 호스트 H1과 H2로 이루어진 간단한 네트워크를 보여준다.

각 라우터의 데이터 평면 역할은 입력 링크에서 출력 링크로 데이터그램을 전달하는 것이다.

네트워크 제어 평면의 근본적 역할은 데이터그램이 송신 호스트에서 목적지 호스트까지 잘 전달되게끔 로컬, 퍼 라우터 포워딩을 조정하는 것이다.

**라우터는 애플리케이션 계층과 트랜스포트 계층을 지원하지 않으므로 프로토콜 스택에서 네트워크 계층의 상위 계층은 존재하지 않는다.**

<br><br>

## 포워딩과 라우팅: 데이터 평면과 제어 평면
<hr style="border-top: 1px solid;"><br>

네트워크 계층의 근본적 역할은 매우 단순하다. 즉, 송신 호스트에서 수신 호스트로 패킷을 전달하는 것이다.

이를 위한 두 가지 네트워크 계층의 중요 기능을 아래와 같이 정의한다.

<br>

+ 포워딩(전달)
  + 패킷이 라우터의 입력 링크에 도달했을 때 라우터는 그 패킷을 적절한 출력 링크로 이동시켜야 한다.
  + 포워딩은 **데이터 평면**에 구현된 하나의 기능(가장 보편적이고 중요한 기능)이다.

<br>

+ 라우팅
  + 송신자가 수신자에게 패킷을 전송할 때 네트워크 계층은 패킷 경로를 결정해야 한다.
  + 이러한 경로를 계싼하는 알고리즘을 라우팅 알고리즘이라 한다.
  + 네트워크 계층의 **제어 평면**에서 실행된다. 

<br>

**포워딩**은 매우 짧은 시간 (보통 몇 나노초) 단위를 갖기에 대표적으로 **하드웨어**에서 실행된다.

반면에, **라우팅**은 네트워크 전반에 걸쳐 출발지에서 목적지까지 데이터그램의 종단간 경로를 결정하는 것이므로, 라우터는 더 긴 시간 (보통 초) 단위를 갖기에 **소프트웨어**에서 보통 실행된다.

운전에 비유하면, A지역에서 B지역으로 갈 때 많은 교차로를 지나게 된다.

이 때 **포워딩**은 한 교차로를 지나는 과정이라 볼 수 있는데 즉, 차가 하나의 도로에서 교차로로 들어서면 교차로를 떠나 어떤 도로로 들어설지를 결정한다.

**라우팅**은 A지역에서 B지역으로의 여행을 계획하는 과정이라 볼 수 있는데 즉, 여행을 시작하기 전에 운전자는 지도를 보면서, 일련의 교차로에 연결된 도로에서 이용 가능한 경로를 선택하는 것이다.

<br>

네트워크 라우터에서 필수 불가결한 요소는 **포워딩 테이블**이다.

**라우터는 도착하는 패킷 헤더의 필드 값을 조사하여 패킷을 포워딩한다.**

이 값을 라우터의 **포워딩 테이블**의 내부 색인으로 사용한다.

포워딩 테이블 엔트리에 저장되어 있는 헤더의 값은 해당 패킷이 전달되어야 할 라우터의 외부 링크 인터페이스를 나타낸다.

<br>

![포워딩 테이블에서 라우팅 알고리즘들의 결정값](https://user-images.githubusercontent.com/52172169/178654774-db068c2e-f5bd-4622-9966-c5d6c24d3a4e.png)

<br>

위의 그림은 그 예시다.

헤더 값이 0110인 패킷이 라우터에 도착한다.

라우터는 자신의 포딩 테이블을 보고 이 패킷에 대한 출력 링크 인터페이스를 결정한다.

헤더값이 0110이면 인터페이스 2로 전달하는 것으로 테이블에 설정되어 있는 걸 볼 수 있다.

<br>

**포워딩은 네트워크 계층 데이터 평면에 의해 실행되는 매우 중요한 기능이다.**

<br><br>

### 제어 평면: 전통적인 접근
<hr style="border-top: 1px solid;"><br>

여기서 어떻게 첫 포워딩 테이블이 구성되는가 의문이 생긴다.

중요한 문제로, 라우팅(제어 평면에서)과 포워딩(데이터 평면에서) 사이의 중요한 상호작용을 보여준다.

<br>

위의 그림에서와 같이 라우팅 알고리즘은 라우터의 포워딩 테이블의 내용을 결정한다.

**라우팅 알고리즘은 각각의 모든 라우터에서 실행되며, 라우터는 포워딩과 라우팅 기능 모두 갖고 있어야 한다.**

한 라우터의 라우팅 알고리즘 기능은 다른 라우터의 라우팅 알고리즘과 소통하며 포워딩 테이블의 값들을 계산한다.

소통은 라우팅 프로토콜에 따라 라우팅 정보에 포함된 라우팅 메시지를 교환하며 이루어진다.

<br><br>

### 제어 평면
<hr style="border-top: 1px solid;"><br>



<br><br>

## 네트워크 서비스 모델
<hr style="border-top: 1px solid;"><br>



<br><br>
<hr style="border: 2px solid;">
<br><br>

# 라우터 내부에는 무엇이 있을까?
<hr style="border-top: 1px solid;"><br>



<br><br>

## 입력 포트 처리 및 목적지 기반 전달
<hr style="border-top: 1px solid;"><br>



<br><br>

## 변환기
<hr style="border-top: 1px solid;"><br>



<br><br>

## 출력 포트 프로세싱
<hr style="border-top: 1px solid;"><br>



<br><br>

## 어디에서 큐잉이 일어날까?
<hr style="border-top: 1px solid;"><br>



<br><br>

### 입력 큐잉
<hr style="border-top: 1px solid;"><br>



<br><br>

### 출력 큐잉 
<hr style="border-top: 1px solid;"><br>



<br><br>

## 패킷 스케줄링
<hr style="border-top: 1px solid;"><br>



<br><br>

### First-In-First-Out
<hr style="border-top: 1px solid;"><br>



<br><br>

### 우선순위 큐잉
<hr style="border-top: 1px solid;"><br>



<br><br>

### 라운드로빈과 WFQ
<hr style="border-top: 1px solid;"><br>



<br><br>
<hr style="border: 2px solid;">
<br><br>

# 인터넷 프로토콜
<hr style="border-top: 1px solid;"><br>



<br><br>

## IPv4 데이터그램 형식
<hr style="border-top: 1px solid;"><br>



<br><br>

## IPv4 데이터그램 단편화
<hr style="border-top: 1px solid;"><br>



<br><br>

## IPv4 주소체계
<hr style="border-top: 1px solid;"><br>



<br><br>

### 주소 블록 흭득
<hr style="border-top: 1px solid;"><br>



<br><br>

### 호스트 주소 흭득: 동적 호스트 구성 프로토콜
<hr style="border-top: 1px solid;"><br>



<br><br>

## 네트워크 주소 변환 (NAT)
<hr style="border-top: 1px solid;"><br>



<br><br>

## IPv6
<hr style="border-top: 1px solid;"><br>



<br><br>

### IPv6 데이터그램 포맷
<hr style="border-top: 1px solid;"><br>



<br><br>

### IPv4에서 IPv6로의 전환
<hr style="border-top: 1px solid;"><br>


<br><br>
<hr style="border: 2px solid;">
<br><br>
