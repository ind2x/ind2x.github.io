---
title : 최장 증가 부분 수열 알고리즘 [Longest Incresing Subsequence]
categories : [Programming, Algorithm]
tags : [Dynamic Programming, 다이나믹 프로그래밍, Longest Incresing Subsequence, LIS]
---

## LIS (Longest Incresing Subsequence)
---
![image](https://user-images.githubusercontent.com/52172169/147819641-fe0332fe-ad90-4158-ae2e-4c2487435d9e.png)

원소의 개수가 n개인 배열에서 값이 증가하는 부분수열 중에서 길이가 가장 긴 부분수열을 찾아내는 알고리즘. 

dp[i] = i번째 원소보다 앞에 있는 원소 중 arr[i]보다 작은 원소의 개수 + 1

```cpp
#include <iostream>
using namespace std;

int dp[1001];  
int arr[1001]; 

int main() 
{
    int n; cin >> n;
    for(int i=0; i<n; i++)
	{
		cin >> arr[i];
	}
	int maxv=1;
	for(int i=0; i<n; i++)
    {
        dp[i]=1;
        for(int j=0; j<i; j++)
        {
            if(arr[j] < arr[i])
            {
                dp[i]=max(dp[i], dp[j]+1);
            }
        }
        maxv=max(maxv, dp[i]);
    }
    cout << maxv << '\n';
    return 0;
}
```

<br>
<br>


