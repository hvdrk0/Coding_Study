# 문제4. [PCCP 기출문제] 2번 / 석유 시추

프로그래머스 레벨 2

https://school.programmers.co.kr/learn/courses/30/lessons/250136

## 문제설명

<img src="https://github.com/user-attachments/assets/13505268-eaf2-41ab-a239-0afd46eb0fcf" alt="image" style="width: 50%; height: 50%;">

검정색 블럭: 석유

관이 지나간 석유 블럭과 그에 인접해 닿을 수 있는 모든 석유 블럭만큼 시추 가능

관의 위치에 따른 시추 가능한 최대값 찾기

### 입력

land : 땅의 정보. [[...], [...], ...]. 0이면 없음, 1이면 있음

### 출력

answer : 시추 가능한 최대값

### 제한사항

<img src="https://github.com/user-attachments/assets/24d9ff90-d080-411c-beae-67c253b66926" alt="image" style="width: 50%; height: 50%;">

효율성도 평가함(런타임)

## 풀이 1. brute force

### 석유 시추 함수 정의

특정 블럭을 시추할 때 인접한 모든 블럭도 시추하는 reculsive 함수

### 관을 모든 위치에 설정하고 최대값 찾기

### 전처리

land는 리스트 형태인데 파이썬 기본 리스트에서는 linked list가 아닌 array list라서 수정할 필요는 없을듯.

c++의 list라면 인덱스 접근에 O(n)이 소요되서 array로 바꾸는게 이득.

### 코드

```
import copy

def solution(land):
    n=len(land)
    m=len(land[0])
    answer = 0
    for i in range(m):
        lands=copy.deepcopy(land)
        ext=0
        for j in range(n):
            ext=extract(lands,[j,i],ext)
        if ext>answer:
            answer=ext
    return answer

def extract(land,loc,extracted):
    total=extracted
    if (loc[0] < len(land) and loc[0] >=0 and
       loc[1] < len(land[0]) and loc[1] >=0
       ):
        if land[loc[0]][loc[1]] != 0:
            total+=1
            land[loc[0]][loc[1]]=0
            neibor=[[loc[0]+1,loc[1]], [loc[0],loc[1]+1],
                   [loc[0]-1,loc[1]], [loc[0],loc[1]-1]]
            for n in neibor:
                total=extract(land,n,total)
    return total
```

### 분석

solution 함수의 outer loop에서 extract는 최대 4mn번 호출

extract에서 재호출 재외 그 자체는 O(1)

해당 과정이 m번 반복되므로 전체 time complexity는 O(m^2 n)

매우 비효율적이고 실제로 정확도는 100이지만 효율성에서 실패

-> Dynamic Programming이나 다른 알고리즘 사용

### Dynamic Programming

#### Optimal substructure?, Overlapping subproblem?

관이  열에 있고, i열 j,k행 만이 석유 블럭이라고 가정하자.

이 때 optimal substructure, overlapping subproblem이 성립한다면 solution=extract_only(i,j)+extract_only(i,k)이다 (각 함수는 독립적으로 시행)

extract_only(i,j)=2, extract_only(i,k)=2인데, solution=2이다.

따라서 모순이고 Dynamic Programming을 사용할 수 없다.

#### 고찰

따라서 알고리즘을 바꾸는 방향으로 진행해야 한다.

우선 land를 탐색한 후에 석유가 있는 block들을 인접한 석유block과 덩어리로 묶는다. 이후 관과 겹치는 묶음을 찾아 그 값을 반환한다

-> 각 block을 node로, 인접한 석유block끼리 edge를 형성한 후 DFS로 덩어리를 만든다?

-> edge를 linked list로 만들고 DFS? edge를 만들 때 바로 처리할 수도 있을듯.

## 풀이 2 덩어리

n*m 배열을 새로 만들고 탐색하면서 덩어리를 만들고 그 index를 배열에 저장

만들어진 덩어리의 석유 개수도 갱신

## 후기


