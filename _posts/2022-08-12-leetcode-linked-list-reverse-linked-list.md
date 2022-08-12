---
title:  "(Leetcode) [Linked List] Reverse linked list"
excerpt: "Given the head of a singly linked list, reverse the list, and return the reversed list."

categories:
  - algorithm
tags:
  - [leetcode, linked list, C++]

permalink: /algorithm/leetcode-linked-list-reverse-linked-list/

toc: true
toc_sticky: true
 
date: 2022-08-12
last_modified_at: 2022-08-12
---

Topic: Linked List  
Difficulty: Easy

### Question
Given the head of a singly linked list, reverse the list, and return the reversed list.
주어진 singly linked list의 head를 이용해서 순서를 뒤바꿔라.

<br>

### My solution: Iterative method
개인적으로 자료구조 중에서 linked list가 제일 쉬운거 같다.

일단 세 개의 temporary 포인터를 생성한다. head 자리에 tempPrev, 그 다음은 temp, 그 다음은 tempNext.  
그리고 두 개의 base case가 있다:
1. head가 nullptr이면 just return nullptr;
2. head->next가 nullptr이면 (node가 하나일 경우) just return head;

내 알고리즘은 temp가 제일 마지막 node까지 이동할 때 까지 node->next를 반대 방향으로 향하게 하는 것이다.  
포인터 두 개로는 불가능하다. 왜냐하면 next의 방향을 뒤바꿔버리면 이동할 수 있는 길이 없어져버리기 때문이다. 그래서 tempNext라는 기준점을 세웠다.

![reverse-linked-list-mysolution.jpg](/assets/images/posts_img/algorithm/reverse-linked-list-mysolution.jpg)

```cpp
#include <iostream>

using namespace std;

struct ListNode {
    int val;
    ListNode *next;
    ListNode() : val(0), next(nullptr) {}
    ListNode(int x) : val(x), next(nullptr) {}
    ListNode(int x, ListNode *next) : val(x), next(next) {}
};

ListNode* reverseList(ListNode* head) {
    if (head == nullptr)
        return nullptr;
    if (head->next == nullptr)
        return head;
    
    ListNode* tempPrev = head;
    ListNode* temp = head->next;
    ListNode* tempNext = head->next->next;

    head->next = nullptr;
    while (temp->next != nullptr) {
        temp->next = tempPrev;
        tempPrev = temp;
        temp = tempNext;
        tempNext = tempNext->next;
    }
    head = temp;
    head->next = tempPrev;

    return head;

}
```

![reverse-linked-list-runtime.png](/assets/images/posts_img/algorithm/reverse-linked-list-runtime.png)

효율성은 확실히 떨어진다. 무언가 더 나은 방법이 있나보다.

<br>

### Alternate solution: Recursion
그래도 학교에서 C++ 과제를 열심히 한 보람은 있나보다. 나의 solution이 geeksforgeeks에서 나오는 첫번째 소개되는 제일 보편화된 solution이었다.  
두번째 방법으론 recursion이 있었다.  
recursion을 이용해서 node를 쪼개고 쪼개 base case를 이용해 마지막 노드를 head로 지정하고, next 포인터의 방향을 뒤집는다.

```cpp
ListNode* reverseList(ListNode* head) {
    if (head==nullptr || head->next==nullptr)
        return head;
    
    ListNode* rest = reverseList(head->next);   // rest는 head로 계속 고정
    ListNode* q = head->next;
    q->next = head;
    head->next = nullptr;

    return rest;
}
```

메모리와 runtime은 첫번째 방법과 큰 차이가 없다.

<br>

### Summary
Reverse linked list에는 크게 두 가지 방법이 있다:
1. pointer 세 개 (prev, curr, next)를 이용
2. recursion