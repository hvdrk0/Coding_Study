# 문제3. [PCCP 기출문제] 1번 / 붕대 감기

프로그래머스 레벨 1

https://school.programmers.co.kr/learn/courses/30/lessons/250137

## 문제설명

붕대감기 : t초동안 붕대를 감으면서 초당 x 만큼 체력 회복. 공격받으면 채널링 끊어짐. 끊기면 처음부터 다시 시작. t초동안 채널링 끊기지 않으면 추가로 y만큼 회복.

1초에 공격받으면 2초부터 다시 시작

최대체력으로 시작

모든 공격이 끝나고 남은 체력 양 확인. 그 전에 죽으면 -1 출력

### 입력

bandage : 붕대감기 스펙. [채널링 시간, 초당 회복량, 추가회복량]

healths : 최대체력

attacks : 공격 정보. [공격시간, 데미지]

### 출력

answer : 남은체력. 만약 죽었으면 -1

### 제한사항

<img src="https://github.com/user-attachments/assets/ecf5c911-16b9-4f63-ba94-386333fda1bf" alt="image" style="width: 50%; height: 50%;">

## 풀이

공격받은 시간 - 마지막 공격 받은 시간 - 1 초동안 붕대 감음 -> 그에 맞는 체력 회복

## 코드

```
def solution(bandage, health, attacks):
    last_attack=0
    hp=health
    for atk in attacks:
        hp=heal(health, hp, atk[0]-last_attack-1, bandage)
        hp-=atk[1]
        last_attack=atk[0]
        if hp<=0:
            hp=-1
            break
    answer = hp
    return answer

def heal(max_hp, hp, time, bandage):
    n=time//bandage[0]
    m=time%bandage[0]
    heals=n*(bandage[0]*bandage[1]+bandage[2]) + m*bandage[1]
    after=hp+heals
    if after>max_hp:
        return max_hp
    else:
        return after
```
## 후기

레벨 1 치고도 좀 쉬운듯

이번에는 헤메지 않고 바로 해서 10분 안에 성공
