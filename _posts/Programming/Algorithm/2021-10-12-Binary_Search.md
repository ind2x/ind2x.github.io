---
title : 이진 탐색 [Binary Search]
categories: [Programming, Algorithm]
tags : [Binary Search, 이진 탐색]
---

## 이진 탐색
```
데이터가 정렬된 배열에서 특정한 값을 찾는 알고리즘.
데이터의 중간에 있는 값을 선택하여 특정 값 x와 비교하고

1. x가 중간 값보다 작으면 중간 값을 기준으로 좌측의 데이터들을 대상으로 탐색
2. x가 중간값보다 크면 배열의 우측을 대상으로 탐색

탐색할 범위를 찾았으면 동일한 방법으로 다시 중간의 값을 임의로 선택하고 비교. 
해당 값을 찾을 때까지 이 과정을 반복.

시간복잡도 : O(log N)
```
<img src="https://mblogthumb-phinf.pstatic.net/MjAxODA0MTdfMjY2/MDAxNTIzOTcxMDkyNzc3.1g_MyAxJjYYUQV5XY1z9eXWwIdfimF9sA3lRT4ZdheEg.k4Y1_tNYbjh1Nlo5_-U95aRI7idqNdD29yubgPPtmn4g.PNG.beaqon/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2018-04-17_%EC%98%A4%ED%9B%84_10.17.56.png?type=w800" style="width: 650px;">

## Code
```c
// 반복문을 이용
int BSearch(int arr[], int target) {
    int start = 0;
    int end = arr.length - 1;
    int mid;

    while(start <= end) {
        mid = (start + end) / 2;

        if (arr[mid] == target)
            return mid;
        else if (arr[mid] > target)
            end = mid - 1;
        else
            start = mid + 1;
    }
    return -1;
}
```
```c
// 재귀문
int BSearchRecursive(int arr[], int target, int start, int end) {
    if (start > end)
        return -1;

    int mid = (start + end) / 2;
    if (arr[mid] == target)
        return mid;
    else if (arr[mid] > target)
        return BSearchRecursive(arr, target, start, mid-1);
    else
        return BSearchRecursive(arr, target, mid+1, end);
}
```

## 백준 1920번 : 수 찾기
Link : <a href="https://www.acmicpc.net/problem/1920" target="_blank">https://www.acmicpc.net/problem/1920</a>
```python
from sys import stdin
n=int(stdin.readline())
A=stdin.readline().split()
m=int(stdin.readline())
check=stdin.readline().split()
A.sort()

for i in check :
    no=True
    start=0
    end=n-1
    while start <= end :
        mid=(start+end)//2
        if A[mid] == i : 
            print(1)
            no=False
            break
        elif A[mid] > i :
            end=mid-1
        else :
            start=mid+1
    if no : print(0)
```

## 출처
<a href="https://cjh5414.github.io/binary-search/" target="_blank">https://cjh5414.github.io/binary-search/</a>  
<a href="https://kosaf04pyh.tistory.com/94" target="_blank">https://kosaf04pyh.tistory.com/94</a>  
