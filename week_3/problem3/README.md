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

#### Time Complexity

for문에서 starting_idx+=1은 총 len(sequence)=n 만큼 실행. 즉, while문 내부는 총 n번 실행되고, 코드 한줄 한줄은 O(1)이므로 while문은 전체 O(n)

나머지 부분은 O(1)이고 n번 반복되므로 O(n)

이전 부분은 O(1)

따라서 전체 O(n)

#### Correctness

while문의 첫째 줄에서 가능한 모든 subsequence가 고려된다

proof)

##### 1. 모든 index i에 대해, i는 한 번 이상 starting_idx인 상태로 while문 첫째 줄을 지난다.

trivial

##### 2. 모든 starting_idx i에 대해, i로 시작하고 합이 k가 되는 모든 subsequence는 while문의 둘째 줄을 지난다.

고려되지 않은 subsequence가 있다고 할 때 해당 subsequence의 시작 인덱스를 s, 끝을 f라고 하자. (s>0)

처음으로 starting_idx=s가 될 때 while문의 마지막 줄을 지났고, 다시 while문의 첫째 줄로 이동한다.

이 때 

1) sum<k인 경우 while문을 빠져나오고 sum>=k가 될 때 까지 for문을 거치며 끝 index를 늘려가고 sum=k가 될 때 while문의 둘째 줄을 지난다 (불가능)

2) sum=k인 경우 trivial하게 불가능

3) sum>k인 경우

starting_idx += 1을 통해 starting_idx가 갱신된다.

이 때 끝 index는 f보다 크고 f+1 (Without Loss of Generality) 라고 하면 직전상태에서 시작index는 s-1, 끝 index는 f+1이다.

loop invariant : 루프 내에서 선택된 sequence는 끝 index를 하나 줄이면 합이 k보다 항상 작다.

initial : 아무것도 선택되지 않았을 때는 trivial. 이후 끝 index=0이 되었을 때 sequence[0] 값과 상관 없이 trivial.

maintenance: 

starting_idx=s', 끝 index=f' 일 때 invariant를 만족하며 루프가 끝났다고 가정하자. 이 때 while문을 빠져나왔으므로 sum = old_sum < k.

다음 루프에 진입해서 끝 index=f'+1이고 sum=old_sum + sequence[f'+1]

이후 while문에서 sum = old_sum + sequence[f'+1] - sequence[s'] - sequence[s'+1] - ... 이므로

sum - sequence[f'+1] = old_sum - ... < k 이다.

terminate : 루프 조건을 만족하며 시작=s'', 끝=len(sequence)-2 = n-2인 상태로 마지막 루프에 진입했을 때 sum=old_sum + sequence[n-1]

이후 while문에서 sum = old_sum + sequence[n-1] - sequence[s''] - sequence[s''+1] - ... 이므로

sum - sequence[n-1] = old_sum - ... < k 이다.

따라서 sum>k도 불가능

모든 경우가 불가능하므로 모든 starting_idx i에 대해, i로 시작하고 합이 k가 되는 모든 subsequence는 while문의 둘째 줄을 지난다.

## 후기

첫 번째 알고리즘은 바로 떠올라서 5분 안에 작업 완료함

다만 실행시간에서 막히고 20분동안 고민했고 겨우 떠올려서 성공함

아예 다른 알고리즘으로 생각했는데 for문에서 넘어갈 때 마다 끝 index를 하나씩 늘려가므로 결국 incremental algorithm의 응용이고, 앞으로 비슷한 상황일 때 incremental 알고리즘을 좀 더 효율적으로 짜도록 시도해 봐야 할듯

찾아보니 두 번째 방법의 이름을 sliding window algorithm이라고 함

