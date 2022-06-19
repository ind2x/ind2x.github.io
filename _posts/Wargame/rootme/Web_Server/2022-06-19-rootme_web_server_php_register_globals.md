---
title: Root-me PHP register globals
date: 2022-06-19-11:43  +0900
categories: [Wargame,Root-me]
tags: [php register_globals]
---

## PHP - register globals
<hr style="border-top: 1px solid;"><br>

```
Author
g0uZ,  8 October 2011

Statement
It seems that the developper often leaves backup files around...
```

<br><br>
<hr style="border: 2px solid;">
<br><br>

## Solution
<hr style="border-top: 1px solid;"><br>

register_globals와 취약점
: <a href="https://stackoverflow.com/questions/3593210/what-are-register-globals-in-php" target="_blank">stackoverflow.com/questions/3593210/what-are-register-globals-in-php</a>
: <a href="https://lactea.kr/entry/php-registerglobals-on-취약점" target="_blank">https://lactea.kr/entry/php-registerglobals-on-취약점</a>

<br>

문제에서 백업 파일이 있다고 했다. 따라서 url 뒤에 ```index.php.bak```을 입력하면 백업파일이 다운로드 된다.

아래는 파일 내용이다.

<br>

```php
<?php


function auth($password, $hidden_password){
    $res=0;
    if (isset($password) && $password!=""){
        if ( $password == $hidden_password ){
            $res=1;
        }
    }
    $_SESSION["logged"]=$res;
    return $res;
}



function display($res){
    $aff= '
	  <html>
	  <head>
	  </head>
	  <body>
	    <h1>Authentication v 0.05</h1>
	    <form action="" method="POST">
	      Password&nbsp;<br/>
	      <input type="password" name="password" /><br/><br/>
	      <br/><br/>
	      <input type="submit" value="connect" /><br/><br/>
	    </form>
	    <h3>'.htmlentities($res).'</h3>
	  </body>
	  </html>';
    return $aff;
}



session_start();
if ( ! isset($_SESSION["logged"]) )
    $_SESSION["logged"]=0;

$aff="";
include("config.inc.php");

if (isset($_POST["password"]))
    $password = $_POST["password"];

if (!ini_get('register_globals')) {
    $superglobals = array($_SERVER, $_ENV,$_FILES, $_COOKIE, $_POST, $_GET);
    if (isset($_SESSION)) {
        array_unshift($superglobals, $_SESSION);
    }
    foreach ($superglobals as $superglobal) {
        extract($superglobal, 0 );
    }
}

if (( isset ($password) && $password!="" && auth($password,$hidden_password)==1) || (is_array($_SESSION) && $_SESSION["logged"]==1 ) ){
    $aff=display("well done, you can validate with the password : $hidden_password");
} else {
    $aff=display("try again");
}

echo $aff;

?>
```

<br>




<br><br>
<hr style="border: 2px solid;">
<br><br>
