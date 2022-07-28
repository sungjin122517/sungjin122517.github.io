---
title:  "(Leetcode) [Graph] Clone graph"
excerpt: "return a deep copy of a connected undirected graph"

categories:
  - algorithm
tags:
  - [leetcode, graph, BFS, C++]

permalink: /algorithm/leetcode_graph_clone_graph/

toc: true
toc_sticky: true
 
date: 2022-07-28
last_modified_at: 2022-07-28
---

### Question
Given a reference of a node in a connected undirected graph, return a deep copy (clone) of the graph.  
Each node in the graph contains a value and a list of its neighbors.

```
class Node {
    public int val;
    public List<Node> neighbors;
}
```

<br>

### Solution
```cpp
Node* cloneGraph(Node* node) {
    if (node==nullptr)
        return nullptr;
    
    // map to keep track of all the nodes which have already been created
    map<Node*, Node*> copies;
    queue<Node*> q;

    q.push(node);
    // copy without its neighbours
    Node* copy = new Node(node->val, {});

    // key = address of original node
    // value = address of new node
    copies[node] = copy;
    while (!q.empty()) {
        Node* u = q.front();
        q.pop();
        vector<Node*> v = u->neighbors;
        for (int i=0; i<v.size(); i++) {
            if (copies[v[i]]==nullptr) {
                // copy = new Node(v[i]->val, {});
                copies[v[i]] = new Node(v[i]->val, {});
                q.push(v[i]);
            }
            copies[u]->neighbors.push_back(copies[v[i]]);
        }
    }
    return copies[node];
}
```

클래스 등장과 그래프에 익숙하지 않은 부분 때문에 지레 겁을 먹고 거의 바로 geeksforgeeks에 찾아봤다. 사실 그래프는 저번 학기 COMP2711 (Discrete mathematics for computer science) 수업을 들으며 기본적인 개념은 익혔다.

이 문제에서 가장 축이 되는 알고리즘은 BFS (Breadth-First Search)이다.  
어떤 한 개의 node를 시작점으로 정해서 모든 node를 traverse 하도록 할 수 있다.  
이 문제에서의 중점은 node를 들를때마다 복제를 하는데, 이미 복제한 node를 재방문할 경우엔 넘어가게끔 해줘야 한다. 이건 노드를 복제할 때마다 map에 저장을 하므로 문제가 되지 않는다.

#### How to keep track of the visited/cloned nodes?
Use of `hashmap/map`. Before adding a node into the map, check if it is already stored in the map.  
*Key*: Address of original node.  
*Value*: Address of cloned node.  

#### How to connect clone nodes?
1. Visit all the neighboring nodes for a node `copy`.
2. For each neighbor of `copy` find the corresponding clone node. If not found, create one.
3. Push the cloned neighbor into the neighboring vector of **cloned version** of `copy`.

![clone-graph.jpg](/assets/images/posts_img/cpp/clone-graph.jpg)

---
### BFS (Breadth-First Search)
시작 노드를 방문한 후 시작 노드에 있는 인접한 모든 노드들을 방문하는 방법.  
더 이상 방문하지 않은 노드가 없을 때까지 BFS가 적용이 된다.  
Queue 자료구조를 이용하여 구현한다. Queue에는 인접 노드들(neighboring nodes)이 저장 된다.

#### 장점
- 출발 노드에서 목표 노드까지의 <mark>최단 길이 경로</mark>를 보장.

#### 단점
- 경로가 매우 길 경우에는 탐색 가지가 급격히 증가함에 따라 보다 많은 기억 공간을 필요.
- 해가 존재하지 않는다면 유한 그래프의 경우, 모든 그래프를 탐색한 후에 실패로 끝난다.
- 무한 그래프의 경우에는 결코 해를 찾지도 못하고, 끝내지도 못한다.

### Reference
<https://www.geeksforgeeks.org/clone-an-undirected-graph/>