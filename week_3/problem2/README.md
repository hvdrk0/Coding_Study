# 문제2. 두 원 사이의 정수 쌍

프로그래머스 레벨 2

https://school.programmers.co.kr/learn/courses/30/lessons/181187

## 문제설명

<img src="https://github.com/user-attachments/assets/2db9179e-5242-4bfb-a806-60b50e2d0523" alt="image" style="width: 50%; height: 50%;">

### 입력

r1, r2 : 작은원, 큰원 반지

### 출력

answer : 두 원 사이 정수쌍 개수


## 풀이

x좌표로 탐색하는데 상하좌우 대칭이므로 (1사분면에서의 개수) * 4 + (x축, y축에서의 개수) 를 하면 됨

### 코드
```
def solution(r1, r2):
    answer = 4 * (r2 - r1 + 1)
    for i in range(1,r1):
        max=int((r2*r2-i*i)**0.5)
        min=ceiling((r1*r1-i*i)**0.5)
        answer += 4 * (max - min + 1)
    
    for i in range(r1,r2):
        max=int((r2*r2-i*i)**0.5)
        answer += 4 * max
        
    return answer

def ceiling(f):
    if f-int(f) > 0:
        return int(f)+1
    else:
        return int(f)
```
#### 분석

각 for문 내부는 O(1)이므로 전체 O(r2)

## 후기

간단한 문제라서 금방 푼듯

ceiling function 라이브러리를 몰랐는데 import math하면 math.ceiling()로 할 수 있음
