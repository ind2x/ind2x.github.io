---
title : "Wechall - Transposition I"
excerpt : "Crypto, Training"
toc: true
toc_sticky: true
categories :
  - Wechall
---

## Crypto - Transposition I
```
It seems that the simple substitution ciphers are too easy for you.
From my own experience 
I can tell that transposition ciphers are more difficult to attack.

However, in this training challenge 
you should have not much problems to reveal the plaintext.
```
```
oWdnreuf.lY uoc nar ae dht eemssga eaw yebttrew eh nht eelttre sra enic roertco drre . Ihtni koy uowlu dilekt  oes eoyrup sawsro don:wo ilsdlsbgad.c
```

## Solution
```
전치암호는 단순하게 글자들의 위치를 서로 바꿔놓은 암호.

암호문의 첫 단어인 oWdnreuf.lY 를 보면 Wonderful임을 유추할 수 있음.
즉, 앞 뒤 자리끼리 서로 바꿔놓은 것이므로 암호화 키는 21, 복호화 키도 21이 됨.
```
```python
cipher='[cipher]'

for i in range(0,len(cipher),2):
    print(cipher[i+1]+cipher[i], end='')
print('')
```
```
Wonderful. 
You can read the message way better when the letters are in correct order. 
I think you would like to see your password now: olidsslgbdac.
```

## 참고
Link : <a href="https://bpsecblog.wordpress.com/2016/08/12/amalmot_3/" target="_blank">bpsecblog.wordpress.com/2016/08/12/amalmot_3/</a>
