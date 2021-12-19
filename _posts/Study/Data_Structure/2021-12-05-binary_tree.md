---
title : "Data Structure : Binary Tree"
categories : [Study, Data Structure]
tags : [Binary Tree, Binary Search Tree, Thread Binary Tree, Balanced Binary Search Tree, Heap]
---

## 이진 트리
```
트리의 모든 노드 차수(자식 노드 개수)를 2 이하로 제한하여, 
전체 트리의 차수가 2 이하가 되도록 정의한 것
```
```
다음과 같은 특징이 있음.

1. 노드가 n개인 이진 트리는 항상 간선이 n-1개이다.

2. 높이가 h인 이진 트리가 가질 수 있는 노드 개수는 
   최소 (h+1)개에서 최대 (2^h+1-1)개이다. (h >= 0)
```

<img src="https://t1.daumcdn.net/cfile/tistory/99E6B23E5B339DBB33">

## 순차 자료구조로 구현한 이진트리
```
이진 트리를 1차원 배열로 표현 시 노드 번호를 배열의 인덱스로 사용.
인덱스 값은 1부터 시작. (root 노드의 인덱스는 1)
```

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FyWpeB%2FbtqEL4vLHlN%2FDif47AZSGkSkmkHh2EvbK0%2Fimg.png"> 

![image](https://user-images.githubusercontent.com/52172169/145019062-b2820a62-b00c-4e58-a0b6-3ea73cda8a84.png) 
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbM4ZHr%2FbtqEKwfU8ng%2FRCyaCjugbzjmdaWfZRbvAk%2Fimg.png">

```
i 번째 노드의 부모 노드 : i//2
i 번째 노드의 왼쪽, 오른쪽 자식 노드 : 2*i, 2*i+1
루트 노드 : 1
```

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdukGrj%2FbtqEKwmKCFo%2FrSACZKaZ7PwzaNfrTgmRj0%2Fimg.png">

```
일차원 배열로는 쉽게 구현 가능하며, 
인덱스 규칙에 따라 부모 노드와 자식 노드를 쉽게 찾을 수 있음.

하지만 편향 이진 트리와 같은 트리는 메모리 낭비가 심해지게 됨.
```

## 연결 자료구조로 구현한 이진트리

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbixGH0%2FbtqEKQkWl1O%2F5q6TESfK5x7HO45yeH1hwK%2Fimg.png">
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fz356F%2FbtqELxysGWC%2FtLYnxuNT9Vcq2M0gq2Lyo0%2Fimg.png">

## 이진트리 순회
```
순회란 모든 원소를 빠트리거나 중복하지 않고 처리하는 연산을 의미함.

이진 트리는 비선형 자료구조이므로 현재 노드를 처리한 후에 어떤 노드를 처리할지
결정하는 기준을 정해 놓은 순회 연산이 필요함.
```
```
순회를 위해 수행할 수 있는 작업은 세 가지로 정의할 수 있음.

D : 현재 노드를 방문하여 처리
L : 현재 노드의 왼쪽 자식 노드로 이동 (왼쪽 서브 트리)
R : 현재 노드의 오른쪽 자식 노드로 이동 (오른쪽 서브 트리)
```
```
위의 세 가지 작업 순서에 따라 세 가지로 구분 할 수 있음.

1. 전위 순회 : DLR 
2. 중위 순회 : LDR
3. 후위 순회 : LRD
```

### 전위 순회 (Preorder Traversal, DLR)
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdKFUGw%2FbtqESVTtY70%2FalR3Hghb4nRJrIcF2mTuX0%2Fimg.png">

### 중위 순회 (Inorder Traversal, LDR)
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FMwhWv%2FbtqETmi1dYl%2FUmitG50hjov3LQl2CJJ8k0%2Fimg.png">

### 후위 순회 (Postorder Traversal, LRD)

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FmLXYK%2FbtqESV62keo%2FySEmIDkEMk14Ouull1d7kk%2Fimg.png">
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FRJMNW%2FbtqFiAgutZe%2FhfmBwK4YSXkjRwXOztKZvk%2Fimg.png">

## Thread 이진 트리
```
이진 트리는 부모 노드와 자식 노드의 이진 트리 기본 구조가 
각 레벨에서 순환적으로 반복하여 전체 트리가 구성되는 구조임.

따라서 각 노드에서의 순회 연산을 재귀호출 방식을 이용해 순환적으로 반복하여
전체 트리에 대한 순회를 처리함.

하지만, 재귀호출 방식은 알고리즘이나 함수 구현은 간단하지만,
성능에서 보면 비효율적일 수 있음. 
```
```
>> 따라서 재귀호출 없이 순회할 수 있도록 수정한 이진트리가 스레드 이진 트리임. <<
```
```
스레드 이진 트리는 자식 노드가 없는 경우에 링크 필드를
널 포인터 대신 순회 순서상의 다른 노드를 가리키도록 설정한 것.

이런 링크 필드를 스레드라고 함.
```

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcaiYnF%2FbtqFgHnoutB%2FB9KVnbWiCBuCS9kvIgQHrk%2Fimg.png">

```
현재 노드 직전에 처리한 노드, 즉 선행자에 대한 포인터는 왼쪽 >> (isThreadLeft)
현재 노드 다음에 처리할 노드, 즉 후행자에 대한 포인터는 오른쪽 >> (isThreadRight)

isThread 필드는 링크 필드가 
자식 노드에 대한 포인터인지, 스레드가 저장되어 있는지 구별하기 위한 태그.
```
```
isThreadLeft 필드가 true -> left 링크 필드는 선행자를 가리키는 스레드가 됨.
isThreadLeft 필드가 false -> left 링크 필드는 왼쪽 자식 노드를 가리키는 포인티가 됨.
```

## 이진 탐색 트리 (BST)
```
이진 탐색 트리는 
이진 트리를 탐색용 자료구조로 사용하기 위해 원소 크기에 따라 노드 위치를 정의한 것임.

-> 이진 탐색 + 이진 트리 = 이진 탐색 트리
```

### 이진 탐색 트리 정의 
```
1. 모든 원소는 서로 다른 유일한 키(고유 값)를 갖는다.

2. 원쪽 서브 트리에 있는 원소들의 키는 그 루트의 키보다 작다.

3. 오른쪽 서브 트리에 있는 원소들의 키는 그 루트의 키보다 크다.

4. 왼쪽 서브 트리와 오른쪽 서브 트리도 이진 탐색 트리이다.

즉, 왼쪽 노드 < 루트 노드 < 오른쪽 노드
```
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FddrD1T%2FbtqEZ0Hm5pb%2F4O5ihaKpJLUaWiSM3mY7dk%2Fimg.png" style="padding-left: 100px;">

### 이진 탐색 트리의 탐색 연산
```
키 값이 x인 원소를 탐색하는 경우

탐색은 항상 루트 노드에서 시작.

1. 키 값과 루트 노드 값 비교
1-1. 키 값 == 루트 노드 값 -> 성공
1-2. 키 값 > 루트 노드 값 -> 오른쪽으로 이동.
1-3. 키 값 < 루트 노드 값 -> 왼쪽으로 이동.

2. 서브 트리로 가서 해당 노드를 루트 노드로 하여 1번 반복.
```
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FuLj1g%2FbtqE0x5y8q9%2Fiewof8ffQUml2yhwT6HeW1%2Fimg.png" style="padding-left : 100px;">

### 이진 탐색 트리의 삽입 연산
```
삽입하려면 이진 탐색 트리에 같은 원소가 있는지 먼저 확인해야 함. (특징 1번)

탐색 성공 시 삽입 연산은 하지 않음.
탐색 실패 시 삽입 연산을 수행하며, 삽입 위치는 실패가 발생한 현재 위치임.
```
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcjTCyN%2FbtqE0kyBrGv%2FJP8RdDMi4RMEfUV2BegAXk%2Fimg.png">


### 이진 탐색 트리의 삭제 연산
```
삭제하려면 이진 탐색 트리에서 삭제할 노드의 위치를 탐색해야 함.

삭제할 노드는 자식 노드 수에 따라 후속 처리를 해줘야 함.

삭제할 노드가 단말 노드인 경우 -> 차수 = 0
삭제할 노드가 자식 노드를 한 개 가진 경우 -> 차수 = 1
삭제할 노드가 자식 노드를 두 개 가진 경우 -> 차수 = 2
```

#### 삭제할 노드가 단말 노드인 경우
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F6XQL4%2FbtqEZMJraru%2FF6Keoo9nRnDEdZ0vDs2Hd0%2Fimg.png">

```
그냥 삭제하면 됨.
```
#### 삭제할 노드가 자식 노드를 한 개 가진 경우
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbGCGUR%2FbtqEZLX05Dn%2FmuggX4SxwWpYnwOl0I1AD1%2Fimg.png">

```
노드 삭제 후 자식 노드로 그 자지를 채우면 됨.
```

#### 삭제할 노드가 자식 노드를 두 개 가진 경우
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbO1HWe%2FbtqE0aQAGzA%2Fn8a1RER4gLRx2DDKy9kqg0%2Fimg.png">

<img src="https://mblogthumb-phinf.pstatic.net/20161012_139/mklmkl2001_14762575571986rTN2_PNG/3.PNG?type=w800">

```
이 경우에는 직계 자식 노드뿐만 아니라 트리 전체에서 찾아야 함.
노드가 삭제되고 자손 노드에게 자리를 물려준 후에도 BST가 유지가 되어야 함.

후계자 노드는 
1. 왼쪽 서브 트리에 있는 노드들의 키 값보다 커야 하고
2. 오른쪽 서브 트리에 있는 노드들의 키 값보다 작아야 함.

따라서 삭제 노드의 
왼쪽 서브 트리에서 가장 큰 자식 노드로 채우거나, 
오른쪽 서브 트리에서 가장 작은 자식 노드로 채워야 함.
```

## 균형 이진 탐색 트리
```
이진 탐색 트리에서 좌우 균형이 잘 맞으면 탐색의 성능이 높아짐.

이러한 원리로 이진 탐색 트리에 왼쪽 서브 트리 높이와 오른쪽 서브 트리 높이에 대한
균형 조건을 추가하여 정의한 트리를 Balanced Binary Search Tree라 함.

대표적으로 AVL 트리, 레드블랙 트리가 있음.
```

레드블랙트리 : <a href="https://zeddios.tistory.com/237" target="_blank">zeddios.tistory.com/237</a>

```
AVL 트리 (Adelson-Velskii, Landis Tree)는 대표적인 균형 이진 탐색 트리임.

AVL 트리는 각 노드에서 왼쪽 서브 트리의 높이 HL과 
오른쪽 서브 트리 높이 HR의 차이가 1 이하인 균형 트리임.

AVL 트리의 특징은 아래와 같음.
```
```
* 왼쪽 서브 트리 < 부모 노드 < 오른쪽 서브 트리

* HL-HR 인 노드의 균형 인수(BF, Balance Factor)를 관리함.

* 각 노드의 균형 인수로 {-1, 0, 1} 값만 가지게 함으로써 
  왼쪽 서브 트리와 오른쪽 서브 트리의 균형을 항상 유지.
```
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbaSvAI%2FbtqE0B05Npb%2FFff5xDKR0JBExvGTWwSlY0%2Fimg.png">

**AVL 트리의 예**
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F1Axz3%2FbtqE0CyWfNa%2FOOIegIzukEwtbFYe596y1K%2Fimg.png">

**비AVL 트리의 예**
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FEnJvm%2FbtqE0OFTmyg%2FQwOhKfyfFSZgyJrN7HeZdK%2Fimg.png">

### AVL 트리 회전 연산
```
AVL 트리가 불균형을 이룬라면 균형으로 맞춰줘야 함.
즉, 삽입 삭제 후 균형 인수를 확인하여 균형을 맞추는 재구성 작업이 필요.
이 작업은 회전 연산을 통해 이루어짐.

불균형 유형에는 4가지가 있음. (LL, RR, LR, RL)
```

#### LL 유형
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FXQtVl%2FbtqEZLKBJZd%2FkDhRBmBoTT1WLD8L0gWH11%2Fimg.png">

#### RR 유형
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FrG1m7%2FbtqEZ08Bl0y%2FrYdfo9VJRcBsCkJE6Z4xD0%2Fimg.png">

#### LR 유형
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbETNyT%2FbtqEZb3P0BL%2Fd9hiXQxFAbIqSYPppoOJg1%2Fimg.png">

#### RL 유형
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FuAGgh%2FbtqEZMQgU81%2FO1fe8JbkNaLLU4jqDQo7q0%2Fimg.png">

## 히프 (Heap)
```
완전 이진 트리 (Complete Binary Tree)

높이가 h이고, 노드 수가 n개일 때 노드 위치가 1번 부터 n번 까지의 위치가
포화 이진 트리와 일치하는 트리.
```
```
힙은 완전 이진 트리에 있는 노드 중에서 
키 값이 가장 큰 노드나 키 값이 가장 작은 노드를 찾기 위해 만든 자료구조.

키 값이 가장 큰 노드를 찾기 위한 히프 -> 최대 히프 (Max Heap)
키 값이 가장 작은 노드를 찾기 위한 히프 -> 최소 히프 (Min Heap)
```
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F1LZ23%2FbtqFcu8Z6pr%2FxukAGlzZGW0Rifg5i4x6Bk%2Fimg.png">

```
최대 힙은 항상 부모 노드 >= 자식 노드인 완전 이진 트리

최소 힙은 항상 부모 노드 <= 자식 노드인 완전 이진 트리
```
**힙이 아닌 트리 예시**  
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FqbDH6%2FbtqFcuOFVCl%2FKoalTUynj6mLQZ5VkkiUkK%2Fimg.png">

### 힙의 삽입 연산
```
완전 이진 트리의 형태 조건을 만족하기 위해서
현재의 마지막 노드의 다음 자리를 확장하여 자리를 생성 후 임시로 저장.

현재 위치에서 최대 힙(최소 힙)인지에 따라 부모 노드와의 값을 비교 후 자리 확정.
```
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FnBUqa%2FbtqFbUmyZP1%2Fg7MrqwEWU61k7hCV7UDlp0%2Fimg.png">

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fd6bHaJ%2FbtqFbB12nff%2FKxsCLWlx40xp1DWrmCxuPK%2Fimg.png">

### 힙의 삭제 연산
```
힙에서 삭제는 언제나 루트 노드에 있는 원소를 삭제하여 반환함.
중요한 것은 루트 노드 삭제 후에도 완전 이진 트리의 형태와 
노드의 키 값에 대한 히프의 조건이 유지되어야 함.
```
```
1. 루트 노드 삭제.

2. 완전 이진 트리 형태 유지를 위해 마지막 노드 삭제.

3. 삭제한 마지막 노드를 루트에 임시 저장.

4. 키 값의 관계가 최대(최소) 힙이 되도록 조정.

5. 임시로 루트에 옮겨논 값과 왼쪽, 오른쪽 자식 노드와 값 비교.

6. 가장 큰(작은) 값과 자리 swap.

7. 다시 자식 노드와 비교 후 6번 실행.
```
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbsFMnv%2FbtqFdK4lu8R%2Fmd5wLDhabSDa6rTAMvz8H0%2Fimg.png">

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fof0KK%2FbtqFdKXzyOs%2FeCrGCTepAZuHsIAI7ukiu0%2Fimg.png">

### 힙의 구현
```
부모 노드의 인덱스 : i//2

왼쪽 자식 노드 인덱스 : i*2

오른쪽 자식 노드 인덱스 : i*2+1
```
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbSQoqe%2FbtqFcNtWnJw%2FWvNfcuAQM6rmPXcDpOphk1%2Fimg.png">

## 참고
Link : <a href="https://foxtrotin.tistory.com/184?category=635012" target="_blank">foxtrotin.tistory.com/184?category=635012</a>  
Link : <a href="https://foxtrotin.tistory.com/187?category=635012" target="_blank">foxtrotin.tistory.com/187?category=635012</a>  
BST : <a href="https://foxtrotin.tistory.com/190?category=635012" target="_blank">foxtrotin.tistory.com/190?category=635012</a>  
AVL : <a href="https://foxtrotin.tistory.com/191?category=635012" target="_blank">foxtrotin.tistory.com/191?category=635012</a>  
Heap : <a href="https://foxtrotin.tistory.com/205?category=635012" target="_blank">foxtrotin.tistory.com/205?category=635012</a>  
