---
title : 소인수분해 알고리즘 [Factorization Algorithm]
categories: [Programming, Algorithm]
tags : [Factorization Algorithm]
---

## 소인수분해
```
소인수분해란 1보다 큰 자연수를 소수의 곱(소수인 인수)으로 나타낸 것.
어떤 수를 소인수분해하려면 2부터 sqrt(N)까지 더 이상 나눌 수 없을 때까지 나눠보면 됨.
>>> 즉, 2로 더 이상 나눌 수 없다면 3으로 나눠보고 .. sqrt(N)까지 반복하면 됨. <<<

자연수 N (N > 1)이 있을 때, 크게 두 가지 경우로 나눌 수 있음.

1. N이 합성수 일 때
1-1. N이 sqrt(N)보다 작거나 같은 소인수들로 이루어진 경우
1-2. sqrt(N)보다 큰 소인수가 있는 경우 -> 이 경우 그 소인수의 지수는 반드시 1임.
     ex) N=28 -> 2^2*7, sqrt(28) = 5.xx --> sqrt(28) < 7 이며 7의 지수는 1임.

2. N이 소수일 때
-> N이 소수이므로 1과 N이 소인수가 되므로 1-2의 경우와 동일한 조건.
```
**sqrt(N)은 함수로 사용해서 할 수 도 있지만 p*p <= N으로 판단하는게 더 빠름.**

## 구현
```cpp
#include <iostream>
#include <vector>
using namespace std;
vector<pair<int, int> > v;

int main(){
    int N; cin >> N;
    for(int p=2; p*p<=N; ++p){
        int cnt=0;
        while(N%p==0){
            N/=p;
            cnt++;
        }
        if(cnt!=0) v.push_back(make_pair(p, cnt));
    }
    if(N != 1) {
        v.push_back(make_pair(N, 1));
    }
    cout << "N의 소인수분해" << '\n';
    for(int i=0; i<v.size(); ++i){
        cout << v[i].first << '^' << v[i].second << '\n';
    }
}
```

## 백준 2312번 : 수 복원하기
```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {
	ios::sync_with_stdio(false); 
    cin.tie(NULL);
	
	int n, t; cin >> t;
	while(t--) {
		vector<pair<int,int>> factors;
		cin >> n;
		for(int i=2; i*i <= n; i++) {
			int cnt=0;
			while(n%i==0) {
				n/=i;
				cnt++;
			}
			if(cnt != 0) {
				factors.push_back(make_pair(i,cnt));
			}
		}
		if(n != 1) {
			factors.push_back(make_pair(n,1));
		}
	
		for(int v=0;v<factors.size(); v++) {
			cout << factors[v].first << ' ' << factors[v].second << '\n';
		}
	}
	return 0;
}
```
