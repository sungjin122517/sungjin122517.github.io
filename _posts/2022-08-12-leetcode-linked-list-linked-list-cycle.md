---
title:  "(Leetcode) [Linked List] Linked list cycle, and unordered set"
excerpt: "Detect loop in a linked list using unordered set"

categories:
  - algorithm
tags:
  - [leetcode, linked list, C++, hashmap, unordered_set]

permalink: /algorithm/leetcode-linked-list-linked-list-cycle/

toc: true
toc_sticky: true
 
date: 2022-08-12
last_modified_at: 2022-08-12
---

Topic: Linked List    
Difficulty: Easy

### Question
Given the head of a singly linked list, determine if the linked list has a cycle in it.  
Linked list에 loop이 있는지 확인해라.

<br>

### Solution
Loop가 존재한다는 뜻은 처음 head부터 쭉 돌았을 때 이미 방문했던 node를 재방문한다는 의미가 된다.  
그러므로 hash table을 이용하면 된다. 여기선 unordered_set을 이용할것이다.  
while loop 안에서 head부터 시작해서 node를 방문할 때마다 set에 저장을 하고, head를 계속 전진시킨다.  
그러면서 현재 노드(head)가 set에 저장되어 있는지를 확인하면 된다.

```cpp
bool hasCycle(ListNode *head) {
    // if (head == nullptr || head->next == nullptr)
    //     return false;
    unordered_set<ListNode*> set;

    while (head != nullptr) {
        // return true if head is found in the set (indicates there is a loop)
        if (set.find(head) != set.end())
            return true;
        
        set.insert(head);
        head = head->next;
    }
    return false;
}
```

<br>

### Set
그야말로 우리가 수학에서 배운 집합이라고 생각하면 된다.

**Features**:
- It does not contain any duplicates (elements are unique).
- Elements are ordered.

### Unordered set
hash table의 한 종류인 unordered set에 대해서 한 번 알아보려 한다.

For an unordered_set, keys are hashed into `indices` of a hash table so that the insertion is always `randomized`.  
It can contain key of any type.  

Average time complexity(for search, insert, and remove): O(1)  
(Why?) It uses hashing to insert elements into buckets. 순서대로 하나하나 다 찾아보는게 아니라 뽑기하는 형식이다.  

Worst case time complexity: O(n), which depends on the internally used hash function.  

**Advantage**: fast insertion and removal.

#### Mainly used methods on unordered sets
- `size` and `empty` for capacity
- `find` for searching a key
  - `find()` function returns an **iterator** to end() if key is not there in set, otherwise an iterator to the key position is returned.
- `insert` and `erase` for modification


#### Sets vs Unordered Sets
**Sets**:
- **ordered** sequence of unique keys.
- (How is it ordered?) Set is implemented as a balanced tree structure.
- Time complexity: O(log n)
  
**Unordered sets**:
- **unordered** (key can be stored in any order) of unique keys. 제일 차별화 되어있는 특징이다.
- Time complexity: O(1)


<br>

### Summary
Linked list에서 cycle을 detect하려면 hash map을 이용해라. 중복되는 node를 찾으면 되기 때문이다.  
무언가 중복되는 element를 찾으려면 hash map을 주로 사용하는 거 같다. 고유한 key에 따른 value를 가지고 있기 때문이다.

<br>

### Reference
<https://www.geeksforgeeks.org/detect-loop-in-a-linked-list/>
<https://www.geeksforgeeks.org/unordered_set-in-cpp-stl/>