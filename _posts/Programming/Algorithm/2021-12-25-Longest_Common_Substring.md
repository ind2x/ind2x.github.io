---
title : 최장 공통 부분 문자열 알고리즘 [Longest Common Substring]
categories : [Programming, Algorithm]
tags : [다이나믹 프로그래밍, Dynamic Programming, Longest Common Substring, 최장 공통 부분 문자열, LCS]
---

## Longest Common Substring
---
Link : <a href="https://www.acmicpc.net/problem/5582" target="_blank">백준 5582번 공통 부분 문자열</a>

![image](https://user-images.githubusercontent.com/52172169/148672661-ab5d3925-2543-4322-a0c7-ea3e5f8d262a.png)

공통 부분 수열과의 차이점은 문자열은 연속되어야 한다는 점임.

따라서 달라져야 하는 부분은 공통 수열에서는 ```arr[i] != arr[j]``` 일 때, 이전까지 구한 부분수열 길이의 최대값을 가져왔지만,

부분 문자열에서는 같지 않을 때, ```dp[i][j]=0```이 되어야 함.

|      |  A   |  C   |  A   |  Y   |  K   |  P   |
| :--: | :--: | :--: | :--: | :--: | :--: | :--: |
|  C   |  0   |  1   |  1   |  1   |  1   |  1   |
|  A   |  1   |  1   |  2   |  2   |  2   |  2   |
|  P   |  1   |  1   |  2   |  2   |  2   |  3   |
|  C   |  1   |  2   |  2   |  2   |  2   |  3   |
|  A   |  1   |  2   |  3   |  3   |  3   |  3   |
|  K   |  1   |  2   |  3   |  3   |  4   |  4   |

```cpp

```

<br>
<br>

## 정리글
---
Link : <a href="https://velog.io/@emplam27/알고리즘-그림으로-알아보는-LCS-알고리즘-Longest-Common-Substring와-Longest-Common-Subsequence" target="_blank">velog.io/@emplam27/</a>
