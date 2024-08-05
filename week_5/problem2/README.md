# 문제2. 

프로그래머스 레벨 2



## 문제설명

시작 시간이 되면 과제 시작

이미 진행 중인 과제는 취소

시간 남으면 최근에 멈춘 것 부터 다시 시작

과제 완료한 순으로 출력

<img src="https://github.com/user-attachments/assets/f02dc2c9-4008-445c-8ad4-6e98f75d93a8" alt="image" style="width: 50%; height: 50%;">

### 입력

plans : [[과제명, 시작시간, 걸리는시간],...]

### 출력

answer : 과제명 완료한 순서대로

### 제한사항

<img src="https://github.com/user-attachments/assets/7aa50a29-94cf-4a60-849d-fc1d87538765" alt="image" style="width: 50%; height: 50%;">

## 풀이


### 코드
```
def solution(plans):
    answer = []
    stack = []
    
    plans=sorted(plans,key=lambda x:x[1])
    for p in plans:
        p[1]=int(p[1][0:2])*60+int(p[1][3:])
        p[2]=int(p[2])
        while len(stack)!=0:
            if (time+stack[-1][-1])>p[1]:
                stack[-1][-1]-=p[1]-time
                time=p[1]
                break
            else:
                answer.append(stack[-1][0])
                time+=stack[-1][-1]
                stack.pop()
        time=p[1]
        stack.append(p)


    for _ in range(len(stack)):
        answer.append(stack.pop()[0])

    return answer
```
#### 분석


## 후기


