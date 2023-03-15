---
title:  "(Leetcode) [Graph, Dijkstra] Path with maximum probability"
excerpt: "Given two nodes start and end, find the path with the maximum probability of success to go from start to end and return its success probability."

categories:
  - leetcode
tags:
  - [leetcode, graph, dijkstra, C++]

permalink: /leetcode/leetcode-graph-path-with-max-prob/

toc: true
toc_sticky: true
 
date: 2023-03-13
last_modified_at: 2023-03-13
---

### Question
<https://leetcode.com/problems/path-with-maximum-probability/>  

<br>

**Topic**: Graph using Dijkstra  

Dijkstra Algorithm  
- shortest path 탐색
- negative weight 포함 불가능
- dynamic programming을 활용
    - 최단거리를 구할 때 그 이전까지 구했던 최단거리 정보를 그대로 사용한다

과정:
1. 시작 노드 설정
2. 시작 노드를 기준으로 각 노드의 minimum weight 저장
3. unvisited node 중에서 minimum weight의 노드를 선택
4. 해당 노드를 거쳐서 특정 노드로 가는 경우를 고려하여 min cost 갱신
5. 3 & 4 반복

<br>

유튜브에서 다익스트라를 이용하기 위한 그래프 클래스와 다익스트라 함수를 만든걸 참고해서 풀었다.  
pair와 priority queue를 사용했다.  
이번 문제는 최대 확률을 찾는 문제여서 다익스트라를 이용하려면 모든 간선(distance)에 -1을 곱해야했다.  
그래야 절대값이 제일 큰 수 (제일 작은 음수)가 큐의 제일 위에 위치하기 때문이다.  
e.g.  top (-0.9, -0.5, -0.1) bottom  

그리고 함수에서 확률을 반환할 때 -1을 곱한 값을 반환하면 된다.  

---
Source code: <https://github.com/sungjin122517/leetcode/blob/main/graph/path-with-max-probability.cpp>  
Reference: <https://www.youtube.com/watch?v=OHJpOGa_L34>