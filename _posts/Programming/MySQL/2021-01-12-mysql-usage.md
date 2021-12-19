---
title : MySQL 사용법 in Linux
categories: [Programming, MySQL]
tags : [MySQL]
---

## root 계정 생성
```
mysqladmin -u {root} password ???
```

## 로그인
```
mysql [OPTIONS] [database]

-p, --password[=name]
                      Password to use when connecting to server. If password is
                      not given it's asked from the tty.

-u, --user=name     User for login if not current user.
```
ex) test db에 접속
```
mysql -u {root} -p test
Enter password : 
```

## Database 생성 및 삭제
**생성**
```
CREATE DATABASE {db name} CHARACTER SET utf8 COLLATE utf8_general_ci;
```
**삭제**
```
DROP DATABASE {db name};
```
**열람**
```
SHOW DATABASES;
```
**선택**
```
USE {db name}

ex) use test
```

## 테이블 생성
```
CREATE TABLE table_name (
    칼럼명1 data_type,
    칼럼명2 data_type
)
```


## 테이블 값 조회
```

```

## 테이블 값 추가
```

```

## 테이블 값 수정
```

```

## 테이블 삭제
```

```