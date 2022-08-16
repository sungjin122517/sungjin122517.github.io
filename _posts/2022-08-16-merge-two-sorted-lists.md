---
title:  "(Leetcode) [Linked List] Merge two sorted lists"
excerpt: "Merge the two lists in a one sorted list"

categories:
  - algorithm
tags:
  - [leetcode, linked list, C++]

permalink: /algorithm/leetcode-linked-list-merge-two-sorted-lists/

toc: true
toc_sticky: true
 
date: 2022-08-16
last_modified_at: 2022-08-16
---

Topic: Linked List  
Difficulty: Easy

### Question
Given the heads of two sorted linked lists, merge them in a one sorted list by splicing together their nodes.

<br>

### Solution
삽질을 엄청나게 했다. 쓸 데 없이 시간을 너무 뺏어먹었다.  
그냥 간단하게 임의의 node를 하나 형성하고, 그 뒤로 순서대로 list에서 node를 빼내와서 이어 붙여서 tempNode.next를 return하면 됐다. 하지만 난 잘못 이해하고 임의의 노드를 형성하면 안 되고 무조건 list1이나 list2 뒤에 이어 붙여서 return 해야하는줄 알았다. 

```cpp
struct ListNode {
    int val;
    ListNode *next;
    ListNode() : val(0), next(nullptr) {}
    ListNode(int x) : val(x), next(nullptr) {}
    ListNode(int x, ListNode *next) : val(x), next(next) {}
};

ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
    if (!list1 && !list2) { return nullptr; }
    if (!list1) { return list2; }
    if (!list2) { return list1; }

    // temporary node to hang the result on
    ListNode dummy;

    // tail points to the last result node
    ListNode* tail = &dummy;
    tail->next = nullptr;

    while (1) {
        ListNode* temp1 = list1;
        ListNode* temp2 = list2;
        if (list1 == nullptr) {
            tail->next = list2;
            break;
        }
        else if (list2 == nullptr) {
            tail->next = list1;
            break;
        }

        if (list1->val <= list2->val) {
            list1 = list1->next;
            tail->next = temp1;
            temp1->next = nullptr;
        }
        else {
            list2 = list2->next;
            tail->next = temp2;
            temp2->next = nullptr;
        }
        tail = tail->next;
    }

    return (dummy.next);
}
```

<br>

### Summary
In order to merge two sorted lists, first create a dummy node, then extract the nodes from two lists according to their value and add them to the end (tail).