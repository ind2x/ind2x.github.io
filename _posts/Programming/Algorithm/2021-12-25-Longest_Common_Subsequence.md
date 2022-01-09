---
title : 최장 공통 부분 수열 알고리즘 [Longest Common Subsequence]
categories : [Programming, Algorithm]
tags : [Longest Common Subsequence, LCS]
---


## LCS (Longest Common Subsequence)
---

![image](https://user-images.githubusercontent.com/52172169/148669138-47614794-7851-44cb-8e8b-5006e5faa0fa.png)

Link : <a href="https://www.acmicpc.net/problem/9251" target="_blank">백준 9251번 : LCS</a>
```cpp
#include <iostream>
#include <string>
using namespace std;

typedef long int li;

li dp[1001][1001];

int main() {
	string arr1, arr2;
	cin >> arr1 >> arr2;
	li i=0, j=0;
	for(; i<arr1.size(); i++) {
		for(j=0; j < arr2.size(); j++) {
			if(arr1[i] == arr2[j]) {
				dp[i+1][j+1] = dp[i][j]+1;
			}
			else {
				dp[i+1][j+1] = max(dp[i][j+1], dp[i+1][j]);
			}
		}
	}
	cout << dp[i][j] << '\n';
	return 0;
}
```

