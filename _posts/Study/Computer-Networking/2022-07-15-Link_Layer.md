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



<br><br>

## 링크 계층 주소체계와 ARP
<hr style="border-top: 1px solid;"><br>



<br><br>

### MAC 주소
<hr style="border-top: 1px solid;"><br>



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
