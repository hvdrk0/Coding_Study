# 문제3. 회전 초밥

백준 실버1

https://www.acmicpc.net/problem/2531

## 문제설명

회전초밥에서 연속으로 k개 접시를 먹고 이 때 받은 쿠폰에 적힌 종류의 회를 추가로 준다고 할 때 먹을 수 있는 초밥 종류의 최댓값 출력

<img src="https://github.com/user-attachments/assets/ff4cae78-f3fa-40cd-890c-417ed4a08f30" alt="image" style="width: 50%; height: 50%;">

### 입력

첫 번째 줄에는 회전 초밥 벨트에 놓인 접시의 수 N, 초밥의 가짓수 d, 연속해서 먹는 접시의 수 k, 쿠폰 번호 c가 각각 하나의 빈 칸을 사이에 두고 주어진다. 

단, 2 ≤ N ≤ 30,000, 2 ≤ d ≤ 3,000, 2 ≤ k ≤ 3,000 (k ≤ N), 1 ≤ c ≤ d이다. 두 번째 줄부터 N개의 줄에는 벨트의 한 위치부터 시작하여 회전 방향을 따라갈 때 초밥의 종류를 나타내는 1 이상 d 이하의 정수가 각 줄마다 하나씩 주어진다.

### 출력

주어진 회전 초밥 벨트에서 먹을 수 있는 초밥의 가짓수의 최댓값을 하나의 정수로 출력한다.

## 풀이

시작 인덱스에서 k개의 접시에서 초밥 종류의 개수를 n,

해당 구간 내에서 c의 개수를 num_c 라고 할 때

num_c가 0보다 크면 n개, 아니면 n+1개이다.

이를 인덱스를 하나씩 늘려가며 최대값을 찾는다.

### 코드
```
from collections import deque

import sys
input = sys.stdin.readline
N,d,k,c = map(int, input().split())
arr = [int(input()) for _ in range(N)]

q=deque()

num_c=0
n=0
temp=0
for i in range(k):
    if arr[i] not in q:
        n+=1
    q.appendleft(arr[i])
    if arr[i]==c:
        num_c+=1
temp=n+int(num_c==0)
ans=temp


j=k-1
for _ in range(N):
    j+=1
    j=j%N
    out=q.pop()
    if out not in q:
        n-=1
    if out == c:
        num_c-=1
    
    if arr[j] not in q:
        n+=1
    q.appendleft(arr[j])
    if arr[j]==c:
        num_c+=1
    temp=n+int(num_c==0)
    if temp>ans:
        ans=temp
    
print(ans)
```
#### 분석

각 for문 내부는 O(1), for문 제외한 부분도 O(1)이므로 전체 time complexity는 O(n)이다.

## 후기

무난한 난이도지만, 백준 첫 문제이다 보니 input에서 헤매고, deque 라이브러리 사용에 시간이 걸림

그냥 바로 list에서 해도 되지만 일단 한번 deque로 해봄

