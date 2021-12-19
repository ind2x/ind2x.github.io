---
title : "Websec - Level 17"
categories : [Wargame, Websec]
tags: [PHP loose comparison vuln]
---

## Level 17
``` php
include "flag.php";

function sleep_rand() { /* I wish php5 had random_int() */
        $range = 100000;
        $bytes = (int) (log($range, 2) / 8) + 1;
        do {  /* Side effect: more random cpu cycles wasted ;) */
            $rnd = hexdec(bin2hex(openssl_random_pseudo_bytes($bytes)));
        } while ($rnd >= $range);
        usleep($rnd);
}

if (isset ($_POST['flag'])):
    sleep_rand(); /* This makes timing-attack impractical. */
                                                 
if (! strcasecmp ($_POST['flag'], $flag))
    echo '<div class="alert alert-success">Here is your flag: <mark>' . $flag . '</mark>.</div>';   
else
    echo '<div class="alert alert-danger">Invalid flag, sorry.</div>';
```

## Solution
```
strcasecmp는 strcmp함수랑 똑같은 함수임. 그냥 ==이 빠진거. 

정리하면 PHP 5.3 버전에서 발생하는 문제로 
인자값에 배열을 넣게되면 NULL 값을 반환해서 
PHP loose comparison vulnerability에 의해 
true를 리턴해서 우회가 가능함.
```
Link : <a href="https://hackability.kr/entry/PHP-strcmp-취약점을-이용한-인증-우회" target="_blank">hackability.kr/entry/PHP-strcmp-취약점을-이용한-인증-우회</a>

"==" 으로 비교할 때
![](https://t1.daumcdn.net/cfile/tistory/2478193352ED08F92B){: .align-center}

"===" 으로 비교할 때
![](https://t1.daumcdn.net/cfile/tistory/211D203752ED093D26){: .align-center}

```
burp suite를 이용해서 flag값을 배열로 바꿔서 주면 된다. 
flag[]=123
```
