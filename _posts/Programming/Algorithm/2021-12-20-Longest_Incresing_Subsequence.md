---
title : 최장 증가 부분 수열 알고리즘 [Longest Incresing Subsequence]
categories : [Programming, Algorithm]
tags : [Dynamic Programming, 다이나믹 프로그래밍, Longest Incresing Subsequence, LIS]
---

## LIS (Longest Incresing Subsequence)
---
Link : <a href="https://www.acmicpc.net/problem/11053" target="_blank">백준 11053번 : 가장 긴 증가하는 부분수열</a>

![image](https://user-images.githubusercontent.com/52172169/147819641-fe0332fe-ad90-4158-ae2e-4c2487435d9e.png)

원소의 개수가 n개인 배열에서 값이 증가하는 부분수열 중에서 길이가 가장 긴 부분수열을 찾아내는 알고리즘. 

증가 부분수열을 찾는 기준은 ```i번째 원소를 기준으로 i번째 원소보다 앞에 있는 원소들 중 arr[i]보다 작은 값의 개수+1```임.

여기서 중복되는 값을 카운트하면 안됨. 

따라서 요점은 arr[i]보다 작은 값 arr[j]를 찾았다면  
j번째 원소까지 고려했을때 만들어진 증가 부분수열 중에서 i번째 원소를 추가했을 때 더 길이가 긴 수열을 dp[i]의 값으로 정하는 것임.

```
dp[i] = i번째 원소보다 앞에 있는 원소 중 arr[i]보다 작은 원소의 개수 + 1

if arr[i] > arr[j] => dp[i]=max(dp[i], dp[j]+1), j <= i
```

아래는 LIS 코드를 구현한 것임.
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

Link : <a href="https://www.acmicpc.net/problem/2565" target="_blank">백준 2565번 : 전깃줄</a>

![image](https://user-images.githubusercontent.com/52172169/147863640-bee2f6c1-b208-454a-8e48-32c17d08ada8.png)

이 문제가 왜 LIS 문제인지 알아야 함.

LIS인 이유는 문제 상의 위치 값을 배열로 나타내면 ```arr[1~10] = {8, 2, 9, 1, 0, 4, 6, 0, 7, 10}```임.  
기본적으로 전깃줄이 교차하지 않으려면 A의 1번 전깃줄은 B의 1번 전깃줄로 가고 2번은 2번으로 .. 해서 10번은 10번으로 평행하게 가는게 일반적임.  

즉, 값이 증가하는 형태로 전깃줄이 이루어져야 한다는 말이 됨. ```{1, 2, 3, 4, 5, 6, 7, 8, 9, 10}```

따라서 ```dp[i] = i번째 전깃줄과 서로 안곂치는 전깃줄의 개수```이며 가장 긴 수열을 찾아내면 되는 것임.

가장 긴 수열이라 함은 서로 안곂치는 전깃줄의 최대 개수이며 이를 전체 전깃줄의 개수에서 빼면 곧 서로 곂치는 전깃줄의 개수를 구할 수 있음.


이와 동일한 문제로 <a href="https://www.acmicpc.net/problem/2352" target="_blank">2352번 : 반도체 설계</a>가 있음. 

하지만 전깃줄 문제는 n의 크기가 100으로 작은편인 반면 반도체 문제는 40000으로 시간초과가 나게 될 것임.  
이 문제는 이분 탐색을 이용해야 함.

<br>
<br>

## 이분탐색을 이용한 LIS
---
아래 링크에서 이분탐색 부분 확인  
Link : <a href="https://jason9319.tistory.com/113" target="_blank">jason9319.tistory.com/113</a>

```cpp
// O(NlogN)

#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;
int main(){
    ios::sync_with_stdio(0); cin.tie(0);
    int N; cin >> N;
    vector<int> v;
    for(int i=0; i<N; ++i){
        int t; cin >> t;
        if(i==0) v.push_back(t);
        else {
            auto it = lower_bound(v.begin(), v.end(), t) - v.begin();
            if(v.size()==it) v.push_back(t);
            
            else if(v[it]>t) v[it]=t;
        }
    }
    cout << v.size() << '\n';
}
```
