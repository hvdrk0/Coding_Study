# 문제3. 연속된 부분 수열의 합

프로그래머스 레벨 2

https://school.programmers.co.kr/learn/courses/30/lessons/178870

## 문제설명

<img src="https://github.com/user-attachments/assets/3541bc7c-ec0f-40b4-9407-5ba55164b806" alt="image" style="width: 50%; height: 50%;">

### 입력

k : 부분수열의 합

sequence : 전체 수

### 출력

answer : 합이 k인 부분수열 중 가장 짧은 것의 시작 인덱스와 마지막 인덱스

## 풀이 1. Incremental Algorithm

기존 수열에서의 solution과 한 원소가 추가될 때 해당 원소를 포함하는 solution의 길이 비교

### 코드
```
def solution(sequence, k):
    answer = [0,0]
    #qwer
    n=len(sequence)+1
    for idx in range(len(sequence)):
        m = incremental(sequence, idx, k)
        if n>m:
            n=m
            answer[0]=idx-n+1
            answer[1]=idx
    return answer

def incremental(sequence, idx, k):
    sum=0
    for i in range(idx,-1,-1):
        if sum < k:
            sum+=sequence[i]
        if sum == k:
            return idx-i+1
        elif sum>k:
            return len(sequence) + 1
    return len(sequence) + 1
        
```
#### 분석

incremental 함수는 O(idx) 만큼 걸리는데 sequence는 모두 자연수이므로 O(min(idx + k))라고 할 수 있음

전체 코드는 O(k*n) 이다.

코드 제출 결과 일부는 런타임이 너무 커서 실패함.

아마 k~=n >> 1 인 경우가 있는듯

따라서 시간 단축 필요

## 풀이2

sequence의 앞에서부터 k 이상이 될 때 까지 원소를 더함.

k와 같으면 해당 인덱스를 저장.

이미 k와 같았던 적이 있다면 subsequence의 길이가 더 짧은 것을 선택

k보다 크면 앞 인덱스부터 버려가면서 k보다 작아질 때 까지 버림.

k보다 작아지면 그때부터 다시 끝 인덱스를 늘려가며 값을 더함

이를 반복해서 마지막 인덱스까지 탐색

### 코드

```
def solution(sequence, k):
    answer = [0,0]
    n=len(sequence)+1
    starting_idx=0
    sum=0
    for i in range(len(sequence)):
        sum+=sequence[i]
        while sum>=k:
            if sum==k and i - starting_idx + 1 < n:
                n=i-starting_idx+1
                answer=[starting_idx,i]
            sum-=sequence[starting_idx]
            starting_idx+=1

    return answer
```
### 분석

#### 증명

loop invariant : 

## 후기

