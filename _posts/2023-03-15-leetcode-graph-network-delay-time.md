---
title:  "(Leetcode) [Graph, Dijkstra] Network delay time"
excerpt: "Given a network of n nodes, return the minimum time it takes for all the n nodes to receive the signal."

categories:
  - leetcode
tags:
  - [leetcode, graph, dijkstra, C++]

permalink: /leetcode/leetcode-graph-network-delay-time/

toc: true
toc_sticky: true
 
date: 2023-03-15
last_modified_at: 2023-03-15
---

### Question
<https://leetcode.com/problems/network-delay-time/>  

<br>

**Topic**: Graph using Dijkstra  

저번에 풀어봤던 Path with maximum probability와 유사한 문제.  
queue(minHeap)을 이용한 구현은 방문 여부를 굳이 체크하지 않아도 된다.  
방문 했으면 nextTime이 이미 업데이트 되었기 때문에 while loop 안에 for loop 안에 if문을 들어가지 않기 때문이다.   

---
Source code: <https://github.com/sungjin122517/leetcode/blob/main/graph/network-delay-time.cpp>    
Reference: <https://www.youtube.com/watch?v=OHJpOGa_L34>