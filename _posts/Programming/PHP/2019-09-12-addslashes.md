---
title : PHP - addslashes()
categories: [Programming, PHP]
tags : [php mb_convert_encoding 취약점]
---

## addslashes()
```php
addslashes ( string $string ) : string

따옴표, 쌍따옴표, 백슬래쉬, NULL 문자에 대해 escape 해주는 함수 

$str = "Is your name O'Reilly?";

echo addslashes($str) // Outputs: Is your name O\'Reilly?
```

### mb_convert_encoding 취약점

멀티바이트 언어에서 유니코드 언어로 변경 시 발생할 수 있는 취약점 : <a href="https://dydgh499.tistory.com/32" target="_blank">https://dydgh499.tistory.com/32</a>  
```
싱글바이트(SBCS) 코드: 모든 캐릭터가 정확히 한바이트 차지한다. 쉽게 설명하자면 프로그래밍 언어에서 char를 생각하면 됨.
(ASCII도 SBCS이다. 문자열의 끝마다 끝을 알리는 NULL,\x00이 반드시 존재한다.)

멀티바이트(MBCS) 코드:MBCS는 2가지 방식이 있는데, SBCS와 DBCS(Double-Byte-CharacherS) 이렇게 두가지 인코딩 방식이 있다. 
영어같이 1바이트를 요구로 하는 문자셋은 SBCS를 사용하고, 한글, 중국어와 같은 2바이트를 요구로 하는 문자셋은 DBCS를 사용한다.
DBCS로 3바이트를 표현할 수도 있지만 아직은 지구상에 3바이트를 표현하는 문자셋이 없기 때문에 표현을 하지 못한다.

유니코드(Unicode):유니코드는 모든 캐릭터 문자셋을 2바이트로 나타내는 표준 인코딩방식이다.


멀티바이트는 1, 2바이트 표현, 유니코드는 모든 문자 2바이트 표현
멀티에서 유니로 인코딩 시 멀티바이트 환경에서 백슬래시 앞에 %a1~%fe의 값이 들어오면 인코딩이 깨지면서 백슬래시를 덮어씌어버려서 
2바이트의 멀티바이트를 하나의 문자(1바이트)처럼 표현이 되는 취약점이 있음.
```

출처: <a href="https://dydgh499.tistory.com/32" target="_blank">https://dydgh499.tistory.com/32 [Creating my everything]</a>
