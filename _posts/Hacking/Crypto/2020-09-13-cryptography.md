---
title : "암호 정리"
author : IND2X
date : 2020-09-13
categories : [Hacking, Crypto]
tags : [Crypto]
---

# 치환암호
참고 : <a href="https://blog.naver.com/PostView.nhn?blogId=wnrjsxo&logNo=221704381990&parentCategoryNo=&categoryNo=2&viewDate=&isShowPopularPosts=true&from=search" target="_blank">blog.naver.com/PostView.nhn?blogId=wnrjsxo&logNo=221704381990&parentCategoryNo=&categoryNo=2&viewDate=&isShowPopularPosts=true&from=search</a>

# Caesar Cipher (seizure cipher)

monoalphabetic cipher(단일문자 치환 암호)
```
간단한 치환암호.
평문의 알파벳들을 각각 일정한 거리만큼 떨어진 다른 알파벳으로 치환.
```

![](https://upload.wikimedia.org/wikipedia/commons/thumb/2/2b/Caesar3.svg/320px-Caesar3.svg.png){: .align-center}

# Vigenere Cipher (polyalphabetic cipher)

다중문자 치환 암호  
<a href="https://ko.wikipedia.org/wiki/비즈네르_암호" target="_blank">ko.wikipedia.org/wiki/비즈네르_암호</a>  

![](https://upload.wikimedia.org/wikipedia/commons/8/8a/%EB%B9%84%EC%A0%9C%EB%84%A4%EB%A5%B4%ED%91%9C_%EC%98%88%EC%8B%9C.png){: .align-center}
![](https://upload.wikimedia.org/wikipedia/commons/1/13/%EC%95%94%ED%98%B8%ED%99%94%EA%B3%BC%EC%A0%95.png){: .align-center}

# DES 

## 구조
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile1.uf.tistory.com%2Fimage%2F9977CE4A5AAEA0891E4A19){: .align-center}

```
Block암호(Feistel 구조), 대칭암호

Plaintext : 64bit
Ciphertext : 64bit
encrypt key : 64bit -> remove parity bit (8) -> 56bit -> key schedule -> 48 bit  


1. 64 bit의 평문을 IP(initial permutation, 초기치환)을 해줌.
2. IP 후 64bit 평문을 32bit씩 L, R로 나눔.
3. R0를 키 스케줄을 통해 나온 48bit 암호키와 같이 F함수에 들어감. -> 32 bit 생성
4. L0와 F함수에서 만든 32bit와 XOR연산
5. 4에서 나온 결과 값은 R1으로, R0은 그대로 L1으로 이동
6. 위 과정을 16라운드 동안 해주고 마지막 라운드에서는 L, R 위치 변경
7. 다시 inverse permutation을 해주면 암호문 64bit 생성
```

### IP(Initial Permutation) table
![](https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcRVRbp0Mt7wLHuaqcbSjxPE_OIdJsr0N9mQ7g&usqp=CAU){: .align-center}


## F함수
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile2.uf.tistory.com%2Fimage%2F994FE4435AAEA2EE02239F){: .align-center}

```
1. R 32bit를 Expansion 해주어서 48bit로 Expansion
2. Expansion R(48bit)와 48bit 암호키 XOR 연산
3. 2의 결과 값 48bit를 8개의 S-box에 6bit씩 넣어줌.
4. S-box에서 규칙에 따라 4bit씩 생성 -> 8*4 = 32bit 생성
5. 32bit를 다시 치환 
6. 32bit F함수 결과값 생성
```

### Expansion Permutation table
![](https://www.tutorialspoint.com/cryptography/images/des_specification.jpg){: .align-center}

### S-Box
```
S-Box 규칙

1. 맨 앞, 뒤 비트를 묶어서 행을 결정 (0~3)
2. 나머지 4비트를 묶어 열을 결정 (0~15)

ex) S-Box 1에 100110이 들어왔다하면 
1. 10 -> 2 (행)
2. 0011 -> 3 (열)
-> S-box 1의 2행 3열 값 8 
-> 8을 다시 2진수로 바꾸면 1000 -> 6bit가 4bit로 변경됨.
```
![](https://3.bp.blogspot.com/-G93D2rfncLk/U8BrCsRR_GI/AAAAAAAAAZ4/wsFHlV4-UT4/s1600/des-s-box2.gif){: .align-center}

## 키 스케줄
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile24.uf.tistory.com%2Fimage%2F997933395AB0D31036179A){: .align-center}

```
1. 64bit의 암호키를 PC-1 전치해줌. -> parity bit 제거(8, 16, 24, 32, 40, 48, 56, 64)
2. 56bit의 키를 Left, Right로 나눠주고 Shift table에 따라 이동
3. PC-2에서 LR을 합쳐 다시 전치 -> 48bit 키 생성
```

### PC-1, PC-2
![](https://regi.tankonyvtar.hu/hu/tartalom/tamop425/0038_matematika_Kalman_Liptai-Cryptography/images/table31.png){: .align-center}

### Shift table
![](https://blackperl-security.gitlab.io/img/post/2016-19-05-amalmot/amalmot-05-04.JPG){: .align-center}

# AES



# RSA
공개키 ```{n, e}```가 있고 개인키 ```{p, q}```가 있음.  
```
RSA 암호화 알고리즘

서로 다른 소수 p, q를 정한 뒤 n, φ(n), e, d를 구한다. 

n = p * q 
φ(n)=(p-1)(q-1)
e : gcd(e, φ(n)) = 1, 1 < e < φ(n)인 e를 정한다.
d : ed=1 mod (φ(n)), 즉 φ(n)에 대한 e의 역원을 구한다. 1 < d < φ(n)

C : Ciphertext, M : Plaintext

encrypt : C ≡ M^e mod (n)
decrypt : M ≡ C^d mod (n)
```
<a href="http://factordb.com/" target="_blank">tool</a>을 이용하여 ```{p, q}```를 구할 수 있음.

# 출처

참고자료 : <a href="https://www.crocus.co.kr/341" target="_blank">crocus.co.kr/3410</a> 
