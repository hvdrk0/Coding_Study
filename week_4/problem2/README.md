# 문제2. 유사 칸토어 비트열

프로그래머스 레벨 2

https://school.programmers.co.kr/learn/courses/30/lessons/148652

## 문제설명

0번째 유사 칸토어 비트열은 1

n번째 비트열은 n-1째 비트열에서 1은 11011, 0은 00000으로 치환

이 때 n번째 비트열에서 l번째부터 r번째까지 1의 개수를 출력

<img src="https://github.com/user-attachments/assets/cbeded07-e652-42f3-bc53-8969b3e727a5" alt="image" style="width: 50%; height: 50%;">

### 입력

n : 비트열 번호

l : 시작 index(1-base)

r : 끝 index(1-base)

### 출력

answer : 구간 내 1 개수

## 풀이

reculsive로 구현

시작 인덱스와 끝 인덱스에 대해 그 parent로 거슬러 올라감

계속 거슬러 올라가면 parent가 겹치게 됨

이 때 해당 parent가 0인지 1인지 판단

0인 조건은 해당 위치에서 계속 parent로 거슬러 올라갈 때 (0-base)index의 mod 5 가 2일 때

판단되고 나면 이후 child에게 정보 반환

다시 child로 내려가면서 parent가 처음으로 겹칠 때 parent가 0이면 이후 child는 전부 0

1이면 시작/끝 인덱스의 mod 5 값에 값 보정.

시작 인덱스의 경우 해당 위치부터 더해가므로 이전 인덱스까지의 값 제거

끝 인덱스의 경우 해당 위치까지 더하므로 이후 인덱스 제거

다시 child로 내려가면 이전 값에 4를 곱하고 마찬가지로 시작/끝 인덱스에 맞춰 값 조정

### 코드
```
def solution(n, l, r):
    answer,_,_ = sol(n,l-1,r-1)  #인덱스를 0-base로 맞춤
    return answer

def sol(n,l,r):
    l1=l//5  #시작부분 parent의 index
    r1=r//5  #끝부분 parent의 index
    l2=l%5 
    r2=r%5
    if n<=0:
        return 1,1,1
    elif l==r:
        if l%5==2:
            return 0,0,0
        else:
            s,l3,r3=sol(n-1,l1,r1)
            return s,l3,r3
    else:
        s,l3,r3=sol(n-1,l1,r1)
        s=s*4-l3*(l2-int(l2>2))-r3*(3-r2+int(r2>=2))
        return s,int(l3 and (l2!=2)),int(r3 and (r2!=2))
```
#### 코드 설명

sol 함수는 solution함수와 마찬가지로 n,l,r을 input으로 받는데 l,r은 0-base이다.

output의 경우 범위 내의 1의 개수, 시작 index의 값, 끝 index의 값 이다.

root의 경우 항상 1,1,1을 출력한다.

처음으로 parent가 같아졌을 때 부터 parent는 l과 r이 같은 값으로 입력되며, 이 때 계속 parent로 거슬러 올라가고 mod 5 == 2가 되면 child는 모두 0,0,0

그렇게 되지 않으면 root 까지 감

그 아래 child로 다시 내려가는데, 우선 1이 11011로 늘어나므로 4배를 해줌

시작index 보정은 l3*(l2-int(l2>2))

설명하면 l3는 시작index의 parent 값이고 0이면 아무것도 하지 않으며, 2인 위치는 값이 0임

끝 index 보정도 비슷

#### 분석

sol 함수의 call은 최대 n번 발생함

각 sol 함수는 call 제외 모두 O(1)임

따라서 전체 time complexity는 O(n)

## 후기

모든 경우 root까지 거슬러 올라간다고 생각하고 구현해서 몇몇 케이스가 오류가 났음

또한 부등호 하나 잘못해서 많이 시간을 소모함

이번에 구현할 때 생각으로만 정리하고 바로 코딩에 들어갔는데 생각하는데 시간이 좀 걸리더라도 미리 다 생각해 놓고 손으로 작성한 후에 코딩하면 실수가 줄어서 시간단축이 가능할듯
