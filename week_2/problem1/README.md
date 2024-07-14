# 문제1. 도넛과 막대그래프

https://school.programmers.co.kr/learn/courses/30/lessons/258711

## 문제설명

도넛모양:simple cycle graph

<img src="https://github.com/user-attachments/assets/011d281f-9d13-4b00-a7cc-0c0fd487bc3e" alt="image" style="width: 50%; height: 50%;">

막대모양

<img src="https://github.com/user-attachments/assets/8fefe073-c5fa-4a88-bec9-750521b8dff6" alt="image" style="width: 50%; height: 50%;">

8자모양

<img src="https://github.com/user-attachments/assets/877a0b36-13e6-45a8-9a6d-eee0e687f39f" alt="image" style="width: 50%; height: 50%;">

위 세 모양의 sub graph들이 있고, 새로운 한 vertex는 각 subgraph에 임의의 한 vertex를 destination으로 하는 edge로 연결되어 있다.

입력은 [[1,2],[3,4]]와 같은 형태로 edges가 주어지며, 출력은 [시작 vertex, #도넛모양, #막대모양, #8자모양]이다.

제한사항

<img src="https://github.com/user-attachments/assets/128b922a-3eee-4af8-94cc-e7e3159a4a50" alt="image" style="width: 50%; height: 50%;">

## 풀이

### 시작 vertex와 각 graph의 특징을 파악

#### 시작 vertex

no incomming edge. only outgoing edges

> 다만, 해당 조건은 막대모양의 시작점도 동일한 특성을 보유.
> 
제한조건에서 그래프의 개수가 2개 이상이므로 starting node는 최소 2개 이상의 outgoing edge를 가지지만, 막대모양의 시작점은 outgoing edge가 한 개 뿐임

#### 그래프

각 그래프의 vertex는 시작 vertex와 incomming edge로 연결될 수도 있으므로 outgoing edge를 기준으로 봐야 함

- **막대모양** : 마지막 vertex는 outgoing edge가 없음

- **8자모양** : intersection vertex 에는 두 개의 outgoing edges가 있음. incomming의 경우 starting vertex와 연결될 경우 

- **도넛모양** : 나머지

### 구현

각 vertex 별로 incomming edge와 outgoing edge의 개수를 구함

이를 바탕으로 starting vertex와 막대모양, 8자모양의 개수를 구하고, 전체 그래프의 개수는 starting vertex의 outgoing edge의 수와 같으므로 이 값에서 두 값을 빼면 도넛모양의 개수를 구할 수 있음

## 코드

def solution(edges):
    incomming, outgoing = counting_edges(edges)
    answer = counting(incomming,outgoing)
    return answer


def counting_edges(E):
    incomming=[0]
    outgoing=[0]
    max_vertex=1
    for e in E:
        if max_vertex < max(e):
            for i in range(max(e)-max_vertex):
                incomming.append(0)
                outgoing.append(0)
            max_vertex=max(e)
        incomming[e[1]-1]+=1
        outgoing[e[0]-1]+=1
    return incomming, outgoing

def counting(incomming, outgoing):
    n=len(incomming)
    zero_incomming_indices=[]
    eight_num=0
    bar_num=0
    for i in range(n):
        if incomming[i]==0:
            zero_incomming_indices.append(i)
        elif outgoing[i]==2:
            eight_num+=1
        elif outgoing[i]==0:
            bar_num+=1
    starting_vertex = max(zero_incomming_indices, key=lambda x: outgoing[x]) + 1
    d_num=outgoing[starting_vertex - 1] - bar_num - eight_num

    return [starting_vertex, d_num, bar_num, eight_num]
    



