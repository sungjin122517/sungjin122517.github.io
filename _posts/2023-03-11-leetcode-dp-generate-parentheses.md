---
title:  "(Leetcode) [DP] Generate Parentheses"
excerpt: "Given `n` pairs of parentheses, write a function to generate all combinations of well-formed parentheses."

categories:
  - leetcode
tags:
  - [leetcode, dp, C++]

permalink: /leetcode/leetcode-dp-generate-parentheses/

toc: true
toc_sticky: true
 
date: 2023-03-11
last_modified_at: 2023-03-11
---

### Question
Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.  
<https://leetcode.com/problems/generate-parentheses/>

<br>

Topic: Dynamic Programming  
전혀 감을 잡지 못 하였다. Solution을 봐도 거의 다 backtracking으로 풀었다.  

답을 보니 생각보다 간단했다.  
Recursion을 이용해서 괄호 앞, 사이, 뒤에 ()을 넣어주면 된다.   
아직 바로 생각해내기엔 한계가 있다.  

Parenthesis 문제의 dp 방법은 사이사이에 () 추가하기.   
메모리는 확실히 적게 먹지만 (Beats 94.2%) 런타임이 길다 (Beats 39.3%).   

unordered set을 이용해서 중복되는 parentheses string을 제거했다.  
그 이후에 vector에 loop을 이용하여 넣어주었다.  

---
Source code: <https://github.com/sungjin122517/leetcode/blob/main/dynamic-programming/generate-parenthesis.cpp>
