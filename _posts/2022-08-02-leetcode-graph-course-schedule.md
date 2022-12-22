---
title:  "(Leetcode) [Graph] Course schedule"
excerpt: "find whether it is possible to finish all courses or not from given dependencies using DFS"

categories:
  - leetcode
tags:
  - [leetcode, graph, DFS, C++]

permalink: /leetcode/leetcode_graph_course_schedule/

toc: true
toc_sticky: true
 
date: 2022-08-02
last_modified_at: 2022-08-02
---

### Question
대학교 수강신청을 예시로 든 문제이다.  
int numCourses: number of courses you have to take  
vector<int> prerequisites[i] = [a, b]: a의 prerequisite는 b이다. 고로 a라는 수업을 들으려면 b를 먼저 들어놔야 한다.  
Return true if you can finish all courses. Otherwise, return false.

### Approach
Consider this problem as a graph.  
e.g. if course `u` is a prerequisite of course `v`, add a directed edge from node `u` to node `v`.  

If a cycle is detected in the graph, then it is not possible to finish all courses. 

<br>

### How to detect cycle in a directed graph?
Use **DFS (Depth First Search)**. DFS for a connected graph produces a tree.  
If there is a `back edge` (self-loop or node to one if its ancestors) present in the graph, there is a cycle in a graph.  

![detect-cycle-in-directed-graph.png](/assets/images/posts_img/algorithm/detect-cycle-in-directed-graph.png)

<br>

### DFS (Depth First Search)
DFS is an algorithm for <mark>traversing or searching tree or graph data structures</mark>.  
Basic idea: start from the root/any arbiytrary node, mark the node and move to the adjacent unmarked node and continue this loop until there is no unmarked adjacent node.  

DFS는 말 그대로 깊이 우선 탐색이다.   
그래프 상에 존재하는 임의의 한 정점으로부터 연결되어 있는 한 정점으로만 나아간다라는 방법을 우선으로 선택한다. 연결할 수 있는 정점이 있을 때까지 계속 연결하다가가 더이상 연결되지 않은 정점이 없으면 바로 그 전 단계의 정점으로 돌아가서 연결할 수 있는 정점이 있는지 살펴본다.  
자료구조는 `stack`을 이용한다.  
<mark>Time Complexity</mark>: O(V+E), where V=number of vertices, E=number of edges.  

#### Algorithm of DFS
Use of recursive function.  
Required features: index of the node and a visited array.
1. Mark the current node as visited.
2. Traverse all the adjacent and unmarked nodes and call recursive function with the index of the adjacent node.

```cpp
class Graph {
public:
    map<int, bool> visited;
    map<int, vector<int>> adj;

    void addEdge(int v, int w) {
        adj[v].push_back(w);    // add w to v's list (edge from v to w)
    }

    void DFS(int v) {
        // return false if it meets a node which was visited (cycle is detected)
        // if (visited[v]==true)
        //     return false;

        // mark the current node as visited
        visited[v] = true;
        cout << v << " ";

        // recur for all the vertices adjacent to this vertex
        vector<int>::iterator i;
        for (i=adj[v].begin(); i != adj[v].end(); i++) {
            if (!visited[*i]) {
                DFS(*i);
            }
        }
    }

}
```

![dfs-visualization](/assets/images/posts_img/algorithm/dfs-visualization.gif)

<br>

### Solution
그래프에서 cycle이 발견되면 false, 아니면 true.

1. Create a unordered map with *key: course*, *value: list of adjacent nodes*.
2. Use vector `visited` to record all the visited nodes.
3. 중간에 false가 하나라도 나오면 dfs 함수 안에 있는 for loop에 인해서 연속으로 false가 나오기 때문에 returns false.

```cpp
bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
    unordered_map<int, vector<int>> adjacencyList(numCourses);
    vector<int> visited(numCourses, 0);
    // vector<int> visited;

    // make list of prerequisites of all courses and add to a map.
    for (int i=0; i<prerequisites.size(); i++) {
        adjacencyList[prerequisites[i][0]].push_back(prerequisites[i][1]);
    }

    // since there may be more than one graph, loop is required.
    for (int i=0; i<numCourses; i++) {
        if (!dfs(i, adjacencyList, visited))
            return false;
    }

    return true;
}

bool dfs(int course, unordered_map<int, vector<int>>& adjacencyList, vector<int> visited) {
    // return false if the node is already visited
    if (visited[course]==1)
        return false;
    // if (find(visited.begin(), visited.end(), course) != visited.end())
    //     return false;
    if (adjacencyList[course].size()==0)
        return true;

    visited[course]=1;     // mark node as visiting
    // visited.push_back(course);
    for (int i=0; i<adjacencyList[course].size(); i++) {
        if (!dfs(adjacencyList[course][i], adjacencyList, visited))
            return false;
    }
    // visited.pop_back();
    adjacencyList[course] = {};
    return true;
}
```

![course-schedule-drawing.jpg](/assets/images/posts_img/algorithm/course-schedule-drawing.jpg)

<br>

### Runtime
![course-schedule-runtime.png](/assets/images/posts_img/algorithm/course-schedule-runtime.png)

유튜브에 neetcode라는 채널에 올라온 풀이를 봤을때 visited라는 list에 방문하고 있는 노드를 추가하고 넣고 하길래 vector push_back과 pop_back을 이용해서 추가하고 넣는 방식 하나와, 그냥 0으로 초기화된 numCourses 사이즈의 vector를 이용해서 방문하고 있는 노드를 1로 바꿔주는 방식 하나를 테스트 해보았다.  
그 결과 넣고 빼는 방식이 runtime이 조금 더 기나 메모리를 확연히 덜 잡아먹는다.

<br>

### 코멘트
시간을 너무 오래 잡아먹었다. 삽질을 너무 많이 했다. 확실히 처음 배우는 DFS라는 개념이라 그렇기도 하고, 집중력도 흐트러졌다. 얼른 다음 문제로 넘어가야겠다.

<br>

### References
<https://www.geeksforgeeks.org/find-whether-it-is-possible-to-finish-all-tasks-or-not-from-given-dependencies/>  
<https://www.youtube.com/watch?v=EgI5nU9etnU>
