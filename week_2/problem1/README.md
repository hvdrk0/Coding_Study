# 문제1. 도넛과 막대그래프
https://school.programmers.co.kr/learn/courses/30/lessons/258711
##문제설명

도넛모양:simple cycle graph

<img src="https://github.com/user-attachments/assets/011d281f-9d13-4b00-a7cc-0c0fd487bc3e" alt="image" style="width: 50%; height: 50%;">

막대모양

<img src="https://github.com/user-attachments/assets/8fefe073-c5fa-4a88-bec9-750521b8dff6" alt="image" style="width: 50%; height: 50%;">

8자모양

<img src="https://github.com/user-attachments/assets/877a0b36-13e6-45a8-9a6d-eee0e687f39f" alt="image" style="width: 50%; height: 50%;">

위 세 모양의 sub graph들이 있고, 새로운 한 vertex는 각 subgraph에 임의의 한 vertex를 destination으로 하는 edge로 연결되어 있다.

입력은 [[1,2],[3,4]]와 같은 형태로 edges가 주어지며, 출력은 [시작vertex, #도넛모양, #막대모양, #8자모양]이다.


##생각



