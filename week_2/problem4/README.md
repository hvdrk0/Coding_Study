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
            neighbor=[[loc[0]+1,loc[1]], [loc[0],loc[1]+1],
                   [loc[0]-1,loc[1]], [loc[0],loc[1]-1]]
            for n in neighbor:
                total=extract(land,n,total)
    return total
```

### 분석

solution 함수의 outer loop에서 extract는 최대 4mn번 호출

extract에서 재호출 재외 그 자체는 O(1)

해당 과정이 m번 반복되므로 전체 time complexity는 O(m^2 n)

매우 비효율적이고 실제로 정확도는 100이지만 효율성에서 실패

-> Memoization 사용 (Dynamic Programming이 아님!! optimal substructure가 성립하지 않음)

## 풀이 2 덩어리

m 길이의 zero list max_ext 생성

land를 탐색하면서 1인 곳이 나오면 추출

이 때 주변부 석유가 존재하면 재귀적으로 추출

최종적으로 덩어리가 만들어짐

이 덩어리의 가로축 좌표의 최대, 최소 사이 index에 대해 덩어리의 크기만큼 모두 max_ext에 더함

### 코드
```
import sys
sys.setrecursionlimit(1000000)

def solution(land):
    n=len(land)
    m=len(land[0])
    max_ext=[0]*m
    
    def extract(i,j,ch):
        land[i][j]=0
        ch[0]+=1
        ch[1]=min(ch[1],j)
        ch[2]=max(ch[2],j)
        if (i!=0) and land[i-1][j]==1:
            extract(i-1,j,ch)
        if (i!=n-1) and land[i+1][j]==1:
            extract(i+1,j,ch)
        if (j!=0) and land[i][j-1]==1:
            extract(i,j-1,ch)
        if (j!=m-1) and land[i][j+1]==1:
            extract(i,j+1,ch)

    for i in range(n):
        for j in range(m):
            if land[i][j]==1:
                chunck=[0,j,j]
                extract(i,j,chunck)
                for k in range(chunck[1],chunck[2]+1):
                    max_ext[k]+=chunck[0]
    answer=max(max_ext)

    return answer
```
### 분석

특정 위치에서 주변 위치에 대해 탐색하는 횟수는 최대 4번

따라서 탐색은 최대 5*m*n회 이하로 일어남

extract함수는 재귀 호출 제외 O(1)이고 메인함수에서 



## 후기


