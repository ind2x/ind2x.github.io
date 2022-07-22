---
title: Link Layer
date: 2022-07-15-15:38 +0900
categories: [Study, Computer Network]
tags: [Link Layer]
---

# 링크 계층 소개
<hr style="border-top: 1px solid;"><br>

링크 계층에서는 데이터그램을 출발지 호스트 노드에서 목적지 호스트 노드까지 전달하기 위해선 개별 링크로 데이터그램을 이동시켜야 한다.

한 링크에서 전송 노드는 데이터그램을 링크 계층 프레임으로 캡슐화해서 링크로 전송한다. 

<br><br>

## 링크 계층이 제공하는 서비스
<hr style="border-top: 1px solid;"><br>

기본 제공 서비스는 데이터그램을 이동시키는 것이고 세부적으로는 아래와 같다.

+ 프레임화

+ 링크 접속 
  + 매체 접속 제어 (Media Access Control, MAC) 프로토콜은 링크상으로 프레임을 **전송**하는 **규칙**에 대해 명시한다.

+ 신뢰적 전달
  + 재전송과 확인응답 기능을 통해 가능하며 주로 오류율이 높은 무선 링크에서 서비스를 제공한다.
  + 오류가 발생하면 종단간에 재전송을 하는 것이 아니라 오류가 발생한 링크에서 오류를 정정한다.
  + 오류율이 낮은 유선 링크(광섬유, 동축케이블 등)에서는 불필요한 오버헤드가 발생하므로 제공하지 않는다. 

+ 오류 검출과 정정
  + 링크계층에서 일반적으로 제공하는 서비스이며, 프레임에 오류 검출 비트를 통해 오류를 검출하고 정정하는 과정은 프레임에 오류가 발생한 곳을 정확하게 찾아 정정한다.

<br><br>

## 링크 계층이 구현되는 위치
<hr style="border-top: 1px solid;"><br>

일반적으로 네트워크 인터페이스 카드(NIC)로 알려진 네트워크 어댑터에 구현된다.

어댑터 중심에는 링크 계층 제어기가 있으며, 제어기는 링크 계층 서비스가 구현되어 있는 특수 용도 칩이다.

따라서 링크 계층 제어기의 기능 대부분은 하드웨어로 구현된다.

<br>

![image](https://user-images.githubusercontent.com/52172169/180366766-70ce164d-76d4-4819-9bc6-52b3a8d464c0.png)

<br>

송신 측 제어기는 데이터그램을 프레임화하고 링크 접속 프로토콜에 따라 링크상으로 전송한다.

수신 측 제어기는 프레임을 수신한 후 네트워크 계층 데이터그램을 추출한다.

링크 계층에서 오류를 검출하는 경우, 송신 측 제어기는 프레임 헤더의 오류 검출 비트를 설정하고 수신 측 제어기는 오류 검출을 수행한다.

<br><br>
<hr style="border: 2px solid;">
<br><br>

# 스위치 근거리 네트워크
<hr style="border-top: 1px solid;"><br>

![image](https://user-images.githubusercontent.com/52172169/180367449-b7c5b903-288a-4ad2-b76b-027782fbe613.png)

<br>

위의 사진에서 4개의 스위치가 2개의 서버와 1개의 라우터, 세 학과를 연결하고 있다.

스위치는 **링크 계층**에서 동작하기 떄문에 프레임을 교환하고, 네트워크 계층 주소를 인식하지 않으며, 라우팅 알고리즘을 사용하지 않는다.

스위치 네트워크에서는 프레임 전달을 위해 IP 주소가 아닌 **링크 계층 주소**를 사용한다.

<br><br>

## 링크 계층 주소체계와 ARP
<hr style="border-top: 1px solid;"><br>

호스트와 라우터들은 링크 계층 주소를 가지는데, 호스트와 라우터는 네트워크 계층 주소도 가지고 있다.

이번에 왜 두 주소가 모두 필요한지와 IP주소를 링크 계층 주소로 변환하는 ARP(Address Resolution Protocol)에 대해 알아본다.

<br><br>

### MAC 주소
<hr style="border-top: 1px solid;"><br>

링크 계층 주소를 가지고 있는건 NIC이다.

NIC가 여러 개면 링크 계층 주소로 여러 개 갖게 된다.

이 주소를 MAC주소(또는 랜 주소)라고 하고 길이는 6바이트이며, 따라서 2^48개만큼의 사용 가능한 랜 주소가 있다.

<br>

![image](https://user-images.githubusercontent.com/52172169/180368982-91dcdc2f-b225-4373-934c-2ece7b914238.png)

<br>

6바이트 주소는 16진수로 표현되고, 주소의 각 바이트는 2개의 16진수로 표시된다.

MAC주소는 고유의 주소를 가지고 있는데 이 부분은 IEEE가 MAC주소 공간을 관리하기 때문이다.

어떤 회사에서 어댑터를 제조하면 2^24개의 주소로 이루어진 주소 영역을 구매해야 한다.

IEEE에서는 MAC주소의 첫 24비트를 고정하고, 나머지 24비트는 회사로 하여금 각 어댑터에게 유일하게 부여하는 방식으로 2^24개 주소를 할당한다.

<br>

송신 어댑터가 프레임을 목적지 어댑터로 전송할 때, 프레임에 목적지 어댑터의 MAC 주소를 넣고 그 프레임을 랜상으로 전송한다.

스위치는 종종 프레임을 자신의 모든 인터페이스로 브로드캐스트한다.

따라서 어댑터는 자신을 목적지로 하지 않는 프레임도 수신할 수 있으며, 수신한 뒤 MAC 주소를 확인하여 목적지 MAC주소가 자신의 MAC주소라면 데이터그램을 추출하고 아니라면 폐기한다.

<br>

만약 송신 어댑터가 랜상의 모든 어댑터가 자신이 전송한 프레임을 수신하기를 원한다면 프레임 목적지 주소에 MAC 브로드캐스트 주소 (FF-FF-FF-FF-FF-FF)를 넣는다.

<br><br>

### ARP
<hr style="border-top: 1px solid;"><br>



<br><br>

### 서브넷에 없는 노드로의 데이터그램 전송
<hr style="border-top: 1px solid;"><br>



<br><br>

## 이더넷
<hr style="border-top: 1px solid;"><br>



<br><br>

### 이더넷 프레임 구조
<hr style="border-top: 1px solid;"><br>



<br><br>

### 이더넷 기술
<hr style="border-top: 1px solid;"><br>



<br><br>

## 링크 계층 스위치
<hr style="border-top: 1px solid;"><br>



<br><br>

### 전달 및 여과
<hr style="border-top: 1px solid;"><br>



<br><br>

### 자가학습
<hr style="border-top: 1px solid;"><br>



<br><br>

### 링크 계층 스위치의 특성
<hr style="border-top: 1px solid;"><br>



<br><br>

### 스위치 vs 라우터
<hr style="border-top: 1px solid;"><br>



<br><br>

## VLAN
<hr style="border-top: 1px solid;"><br>



<br><br>
<hr style="border: 2px solid;">
<br><br>

# 총정리: 웹페이지 요청에 대한 처리
<hr style="border-top: 1px solid;"><br>



<br><br>

## DHCP, UDP, IP 그리고 이더넷
<hr style="border-top: 1px solid;"><br>



<br><br>

## DNS와 ARP
<hr style="border-top: 1px solid;"><br>



<br><br>

## DNS 서버로의 인트라-도메인 라우팅
<hr style="border-top: 1px solid;"><br>



<br><br>

## TCP와 HTTP
<hr style="border-top: 1px solid;"><br>



<br><br>
<hr style="border: 2px solid;">
<br><br>
