# 문제1. 요격 시스템

프로그래머스 레벨 2

https://school.programmers.co.kr/learn/courses/30/lessons/181188

## 문제설명

미사일은 [시작x좌표, 끝x좌표] 형태로 나타냄

요격미사일은 해당 x좌표에 있는 모든 미사일을 요격함(단, 정확히 시작좌표와 끝좌표면 요격 불가)

필요한 요격 미사일의 최솟값

<img src="https://github.com/user-attachments/assets/be8bc775-2a8c-423e-a318-786a9b65f5c2" alt="image" style="width: 50%; height: 50%;">

### 입력

targets : 미사일 정보. [[시작,끝], [시작,끝], ...]

### 출력

answer : 필요한 요격 미사일 수의 최솟값

### 제한사항

<img src="https://github.com/user-attachments/assets/5cca31b7-c569-4cd4-959a-d1110a46a3b5" alt="image" style="width: 50%; height: 50%;">

## 풀이

끝 좌표 순서로 sort하고 cover되지 않은 미사일의 끝좌표보다 약간 앞(epsilon, e)에 요격 미사일을 배치(Greedy Algorithm)

### Greedy Algorithm 증명

#### Greedy Choice Property

sorted_targets T에서 T[0]의 끝점의 좌표를 T[0].f, 시작점의 좌표를 T[0].s라고 하고 greedy choice에 의해 선택된 첫 번째 좌표는 g0 = T[0].f-e, 이 좌표를 포함하지 않는 optimal한 요격 미사일 좌표의 set을 M 이라고 하자.

이 때 M은 T[0]를 cover하므로 M[0]<T[0].f이고 M[0] < g0 < T[0].f 이다. (without loss of generality)

M에 의해 cover되는 미사일의 set을 MT(=T), M[0]에 의해 cover되는 미사일의 set을 MT0, g0에 의해 cover되는 미사일의 set을 GT0라고 할 때,

M0[0].s <= M0[1].s <= ... <. M0[-1].s < M[0] < g0 < M0[0].f = T[0].f 이므로 MT0 ⊂ GT0 이다.

M' = {M-M[0]} ∪ {g0} 일 때 M'에 의해 cover되는 미사일의 set을 M'T라고 할 때, 

|T| = |MT| = |MT - MT0 ∪ MT0| <= |MT - MT0 ∪ GT0| = |M'T| <= |T| 이므로 |M'T| = |T| 이다.

또한 |M| = |M'| 이므로 M' 역시 optimal solution 이고, greedy choice에 의해 선택된 g0를 포함하는 optimal solution은 항상 존재한다.

따라서 Greedy Choice Property가 성립

#### Optimal Substructure

### 코드

```

```

### 분석



#### 고찰



## 후기


