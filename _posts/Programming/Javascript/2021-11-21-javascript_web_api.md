---
title : Javascript Web API
categories: [Programming, Javascript]
---

## XMLHttpRequest
```javascript
client=new XMLHttpRequest();
client.open('POST', "https://www.wechall.net/challenge/wannabe7331/limited_access/protected/protected.php", true)
client.setRequestHeader('Content-Type','application/x-www-form-urlencoded');
client.send();
```
