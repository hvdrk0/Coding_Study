# 문제4. [PCCP 기출문제] 2번 / 석유 시추

프로그래머스 레벨 2

https://school.programmers.co.kr/learn/courses/30/lessons/250136

## 문제설명

<img src="https://github.com/user-attachments/assets/13505268-eaf2-41ab-a239-0afd46eb0fcf" alt="image" style="width: 50%; height: 50%;">

검정색 블럭: 석유

관이 지나간 석유 블럭과 그에 인접해 닿을 수 있는 모든 석유 블럭만큼 시추 가능

관의 위치에 따른 시추 가능한 최대값 찾기

제한사항

<img src="https://github.com/user-attachments/assets/24d9ff90-d080-411c-beae-67c253b66926" alt="image" style="width: 50%; height: 50%;">

효율성도 평가함(런타임)

## 풀이 1. brute force

### 석유 시추 함수 정의

특정 블럭을 시추할 때 인접한 모든 블럭도 시추하는 reculsive 함수

### 관을 모든 위치에 설정하고 최대값 찾기

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

solution 함수의 outer loop에서 extract는 최대 mn번 호출

extract 그 자체는 O(1)

해당 과정이 m번 반복되므로 전체 time complexity는 O(m^2 n)

매우 비효율적이고 실제로 정확도는 100이지만 효율성에서 실패

-> Dynamic algolitm이나 다른 알고리즘 사용

### Dynamic Algoritm

#### Optimal substructure?, Overlapping subproblem?

관이 i째 열에 있고, i열 j,k행 만이 석유 블럭이라고 가정하자.

이 때 optimal substructure, overlapping subproblem이 성립한다면 solution=extract_only(i,j)+extract_only(i,k)이다 (각 함수는 독립적으로 시행)

extract_only(i,j)=2, extract_only(i,k)=2인데, solution=2이다.

따라서 모순이고 Dynamic Programming을 사용할 수 없다.

#### 고찰

따라서 알고리즘을 바꾸는 방향으로 진행해야 한다.

## 풀이 2. DFS

각 block을 node로 놓고 

## 후기

1시간이나 걸렸음. 생각보다 오래걸림

문제 구상할 때 DFS로 풀려고 해서 시작이 꼬인게 큰 듯

DFS로 할 수는 있지만 지금 푼 풀이보다 복잡하고, 어차피 해당 사고를 포함할 것으로 추정

또한 코드 구현에도 좀 헤맨 감이 있는데 기본기가 모자란 것 같으니 레벨 1과 2를 병행하는 방향으로 잡을 예정
