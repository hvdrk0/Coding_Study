# 문제2. 가장 많이 받은 선물

프로그래머스 레벨 1

[https://school.programmers.co.kr/learn/courses/30/lessons/258711](https://school.programmers.co.kr/learn/courses/30/lessons/258712)

## 문제설명

두 사람이 선물을 주고받은 기록이 있다면, 이번 달까지 두 사람 사이에 더 많은 선물을 준 사람이 다음 달에 선물을 하나 받음

두 사람이 선물을 주고받은 기록이 하나도 없거나 주고받은 수가 같다면, 선물 지수가 더 큰 사람이 선물 지수가 더 작은 사람에게 선물을 하나 받음

선물지수: #준선물 - #받은선

두 사람의 선물 지수도 같다면 다음 달에 선물을 주고받지 않음

다음달에 선물을 가장 많이 받을 친구가 받을 선물의 수 구하기

### 입력

friends : 사람 이름. ['a','b',...]

gifts : 선물 주고 받은 기록. ['준사람 받은사람', '준사람 받은사람' ,...]

### 출력

answer : 다음달에 선물을 가장 많이 받을 친구가 받을 선물의 수

### 제한사항

<img src="https://github.com/user-attachments/assets/a5e8b964-1fe5-4f2a-826c-6e8cefe082d4" alt="image" style="width: 50%; height: 50%;">

## 풀이

### 전처리?

입력 gifts를 다루기 편하게 변환

['준사람 받은사람', '준사람 받은사람' ,...] 을 [[준사람index, 받은사람index], [준사람index, 받은사람index], ...] 형태로 변환

우선 string을 ' '기준으로 나누고 index로 바꾸기

### 선물 기록 정리

누가 누구에게 몇개를 받았는지 n * n 행렬로 재구성, 선물지수 계산

행렬에서 row : 받은 사람, column : 준 사람

### 계산

행렬과 선물지수를 이용해 모든 사람의 pair에서 누가 받을지를 계산

### 출력

가장 많이 받는 사람의 선물 개수를 출력

## 코드

```
import numpy as np

def solution(friends, gifts):
    n=len(friends)
    splited_string=split(gifts)
    splited=translation(friends, splited_string)
    recieved,total= make_array(splited,n)
    recieve=cal(recieved,total)
    answer = max(recieve)
    return answer

def split(gifts):
    splited_string=[gift.split(' ',1) for gift in gifts]
    return splited_string

def translation(friends, 것
