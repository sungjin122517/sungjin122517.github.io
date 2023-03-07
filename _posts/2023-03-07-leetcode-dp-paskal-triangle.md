---
title:  "(Leetcode) [DP] Pascal's Triangle"
excerpt: "Given an integer `numRows`, return the first numRows of Pascal's triangle."

categories:
  - leetcode
tags:
  - [leetcode, dp, C++]

permalink: /leetcode/leetcode-dp-pascals-triangle/

toc: true
toc_sticky: true
 
date: 2023-03-07
last_modified_at: 2023-03-07
---

### Question
Given the root of a binary tree, return its maximum depth.  
<https://leetcode.com/problems/pascals-triangle/>


<br>

DP 문제.  
2D vector를 이용한다.  
삼각형의 각 층을 갯수에 맞춰서 1로 초기화한다.  
전 층의 숫자들을 계산해서 현재 층의 vector element들을 업데이트 시켜준다.  

time complexity: O(N^2)
space complexity: O(N)

---
Source code: <https://github.com/sungjin122517/leetcode/blob/main/dynamic-programming/pascals-triangle.cpp>