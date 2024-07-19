# 문제1. 요격 시스템

프로그래머스 레벨 2

https://school.programmers.co.kr/learn/courses/30/lessons/181188

## 문제설명

미사일은 [시작x좌표, 끝x좌표] 형태로 나타냄

요격미사일은 해당 x좌표에 있는 모든 미사일을 요격함

필요한 요격 미사일의 최솟값

<img src="https://github.com/user-attachments/assets/be8bc775-2a8c-423e-a318-786a9b65f5c2" alt="image" style="width: 50%; height: 50%;">

### 입력

targets : 미사일 정보. [[시작,끝], [시작,끝], ...]

### 출력

answer : 필요한 요격 미사일 수의 최솟값

### 제한사항

<img src="https://github.com/user-attachments/assets/5cca31b7-c569-4cd4-959a-d1110a46a3b5" alt="image" style="width: 50%; height: 50%;">

## 풀이

끝 좌표 순서로 sort하고 끝좌표와 그보다 앞에있는 다음 미사일의 시작좌표중 최대값 사이에 요격 미사일을 배치(Greedy Algorithm)

### 코드

```

```

### 분석



#### 고찰



## 후기


