Topic: Tree  
Difficulty: Easy

---
### Question
Given the root of a binary tree, return its maximum depth.

<br>

### Solution 1: Recursion
Recursion을 써야한다는 문제인건 알았지만, 아직까지도 재귀 함수는 내 머리로 구현하기는 어렵다.  
재귀법을 이용해서 subtree의 노드에 left와 right의 depth를 구하고, 그 노드의 height를 max(left depth, right depth)+1로 지정한다.  
이렇게 되면 root로 올라갈 때까지 depth가 계속 1씩 증가하게 된다.

```cpp
int maxDepth(TreeNode* root) {
    if (!root)
        return 0;
    
    int leftDepth = maxDepth(root->left);
    int rightDepth = maxDepth(root->right);

    if (leftDepth>rightDepth)
        return leftDepth+1;
    else 
        return rightDepth+1;
}
```

Recursion method는 코드가 짧고 간결하지만 runtime이 길고 메모리를 많이 잡아먹는다.  

<br>

### Solution 2: BFS (level order traversal)
두번째 방법은 너비 우선 탐색(BFS)이다. 그래프 문제에서 다룬적이 있다.  
root부터 시작해서 depth를 하나씩 늘려간다.  
queue에는 특정 레벨의 노드들을 담아두고, 다음 레벨로 넘어갈 땐 node를 지워준다. 더이상 child들이 없으면 depth 증가는 끝이 난다.  
처음에 queue에 root를 담아두고 시작을 한다. 만약 노드에 child가 있으면, 자기 자신은 pop()을 이용해서 제거하고 자기의 child들을 queue에 담는다. 그리고 depth를 증가시킨다.  

```cpp
int maxDepth(TreeNode* root) {
    if (!root)
        return 0;
    
    queue<TreeNode*> q;
    q.push(root);
    int depth = 0;

    int qSize = q.size();
    while (!q.empty()) {
        for (int i=0; i<qSize; i++) {
            TreeNode* temp = q.front();
            q.pop();
            if (temp->left)
                q.push(temp->left);
            if (temp->right)
                q.push(temp->right);
        }
        depth++;
    }
    
    return depth;
}
```

![max-depth-of-binary-tree-diagram.jpg](/assets/images/posts_img/algorithm/max-depth-of-binary-tree-diagram.jpg)