---
title:  "(Leetcode) [Graph] Pacific Atlantic water flow"
excerpt: "find whether it is possible to finish all courses or not from given dependencies using DFS"

categories:
  - algorithm
tags:
  - [leetcode, graph, BFS, C++]

permalink: /algorithm/leetcode-graph-pacific-atlantic-water-flow/

toc: true
toc_sticky: true
 
date: 2022-08-09
last_modified_at: 2022-08-09
---

### Question
`m x n` 직사각형의 섬이 있는데, 좌측과 상단은 태평양으로 둘러싸여져있고 우측과 하단은 대서양으로 둘러싸여져있다.  
섬은 정사각형의 셀로 나뉘어진다. `heights`라는 정수 매트릭스에서 `heights[r][c]`에 적혀있는 정수는 `(r, c)` 좌표의 해발고도를 나타낸다.  
섬에는 비가 많이 오는데, 기준 셀의 동서남북에 있는 셀들의 높이가 기준 셀의 높이보다 낮으면 비가 흘러 내려간다. 그리고 대양에 접해있는 셀들에서는 비가 무조건 대양으로 흘러 내려간다.  
우리의 목표는 빗물이 태평양과 대서양 **두 군데 다**로 흘러갈 수 있는 셀의 좌표를 result라는 벡터에 push하는 것이다.

<br>

### My first approach
<!-- 일단 첫번째로 각 셀의 좌와 상을 비교해서 현재 셀보다 숫자가 작으면 recursion을 이용해서 계속 비교하게 한다.
만약 Pacific Ocean으로 빠지면 true가 return 될 것이므로 그 다음엔 우와 하를 비교해서 Atlantic Ocean으로까지 빠지나 비교했다.
사실 두 개의 함수 이름을 dfsPacific과 dfsAtlantic으로 지었지만 내가 코드를 작성한게 dfs개념이 맞는진 잘 모르겠다.
코드를 돌려본 결과 이름 모를 에러가 뜬다.

runtime error: reference binding to misaligned address 0xbebebebebebebec2 for type 'int', which requires 4 byte alignment (stl_vector.h)
0xbebebebebebebec2 -->

함수 두 개를 만들었다. 각 셀이 Pacific Ocean으로 갈 수 있는지를 확인하는 bool dfsPacific과, Atlantic Ocean으로 갈 수 있는지를 확인하는 bool dfsAtlantic. base case들은 row와 column의 좌표를 이용해서 물이 Pacific이나 Atlantic에 도달했는지를 확인해서 return true하고, 그리고 Pacific 같은 경우는 좌&상 방향, Atlantic 같은 경우는 우&하 방향의 셀 숫자와 비교해서 물이 이동할 수 없으면 return false 하게끔 설계를 해놨다.  
사실 함수 이름들에 dfs를 넣긴 했지만 내가 작성한 코드가 dfs개념을 잘 사용한거 같지는 않다.

#### 문제점
일단 코드는 돌아간다. 하지만 경우에 따라서 예를 들어 물의 방향이 계속 한 방향으로만 가면 도달하지 못 할수도 있지만 상하좌우를 왔다갔다하며 움직이면 도달할 수 있는 경우가 있다. 이런 문제점에 해결방법이 dfs가 될 거 같지만 갈피를 못 잡겠다.

<br>

### Solution
어김없이 geeksforgeeks에서 해설을 읽어봤다.  
DFS나 BFS 둘 다 사용할 수 있다고 한다. 하지만 해설에선 BFS에 대한 풀이가 있어서 참고해서 쓴다.  
일단 내가 생각했던 일단 Pacific과 Atlantic을 따로 보고 문제를 해결해야 한다.
1. Create two queues; each for storing the coordinates **directly connected to** the Pacific Ocean and the Atlantic Ocean.
2. Create two vectors for each marking the visited coordinates during the BFS traversal from all the coordinates in two queues.
3. Coordinates that are marked as visited in both the vectors are added in the result.

```cpp
vector<vector<int>> pacificAtlantic(vector<vector<int>>& heights) {
    vector<vector<int>> result;
    queue<pair<int, int>> qPac, qAtl;
    int row = heights.size();
    int col = heights[0].size();

    for (int i=0; i<col; i++) {
        qPac.push({0, i});
        qAtl.push({row-1, i});
    }
    for (int j=0; j<row-1; j++) {
        qPac.push({j+1, 0});
        qAtl.push({j, col-1});
    }

    vector<vector<bool>> visitedP(row, vector<bool>(col, false));
    vector<vector<bool>> visitedA(row, vector<bool>(col, false));

    BFS(heights, visitedP, qPac, row, col);
    BFS(heights, visitedA, qAtl, row, col);

    for (int i=0; i<row; i++) {
        for (int j=0; j<col; j++) {
            if (visitedP[i][j] && visitedA[i][j]) {
                result.push_back({i, j});
            }
        }
    }

    return result;
}

// function to check if coordinate (i, j) lies inside N*M matrix
bool safe(int i, int j, int row, int col) {
    if (i<0 || j<0 || i>=row || j>=col)
        return false;
    return true;
}

// perform BFS traversal and mark visited cells
void BFS(vector<vector<int>> heights, vector<vector<bool>> &visited, queue<pair<int, int>> q, int row, int col) {
    while (!q.empty()) {
        pair<int, int> cur = q.front();
        q.pop();
        visited[cur.first][cur.second] = true;

        // check right side of the cell and see if right cell can reach the current cell
        if (safe(cur.first+1, cur.second, row, col) && heights[cur.first+1][cur.second] >= heights[cur.first][cur.second]
        && visited[cur.first+1][cur.second]==false) {
            q.push({cur.first+1, cur.second});
            visited[cur.first+1][cur.second] = true;
        }
        // check left ...
        if (safe(cur.first-1, cur.second, row, col) && heights[cur.first-1][cur.second] >= heights[cur.first][cur.second]
        && visited[cur.first-1][cur.second]==false) {
            q.push({cur.first-1, cur.second});
            visited[cur.first-1][cur.second] = true;
        }
        // check down ...
        if (safe(cur.first, cur.second-1, row, col) && heights[cur.first][cur.second-1] >= heights[cur.first][cur.second]
        && visited[cur.first][cur.second-1]==false) {
            q.push({cur.first, cur.second-1});
            visited[cur.first][cur.second-1] = true;
        }
        // check up ...
        if (safe(cur.first, cur.second+1, row, col) && heights[cur.first][cur.second+1] >= heights[cur.first][cur.second]
        && visited[cur.first][cur.second+1]==false) {
            q.push({cur.first, cur.second+1});
            visited[cur.first][cur.second+1] = true;
        }
    }
}
```

![pacific-atlantic-water-flow-drawing.jpg](/assets/images/posts_img/algorithm/pacific-atlantic-water-flow-drawing.jpg)