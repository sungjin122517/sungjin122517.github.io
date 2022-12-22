---
title:  "(Leetcode) [Dynamic programming]: Climbing stairs"
excerpt: "count ways to reach the n'th stair by using dynamic programming"

categories:
  - leetcode
tags:
  - [leetcode, dynamic programming, C++]

permalink: /leetcode/leetcode_dp_climbing_stairs/

toc: true
toc_sticky: true
 
date: 2022-07-20
last_modified_at: 2022-07-20
---

Topic: Dynamic programming  
Difficulty: Easy

### Question
Find the number of distinct ways of climbing up the stairs of n steps to the top. We can either climb 1 or 2 steps.

<br>

### My first solution
1. 일단 모든 step이 한 걸음일 때를 미리 카운트 한다. int count = 1;
2. step=2가 포함될 수 있는 최대 개수를 찾는다. int max_two = n/2;
3. 루프를 이용해서 각기 다른 2의 개수와 1의 개수로 만들 수 있는 조합을 factorial을 이용해서 찾는다. 그리고 카운트에 더해준다.

이 알고리즘은 효율성이 완전 꽝이다. 난 팩토리얼 구하는 라이브러리가 있을 줄 알았는데 C++에는 없다고 한다. 그래서 팩토리얼을 따로 구해야 하는데, 팩토리얼 구하는 것도 루프가 사용되기 때문에 이중 루프가 만들어지게 되므로 time complexity가 O(n^2)이다. 

<br>

### Second solution: use of recursion (without dynamic programming)
geeksforgeeks에서 아이디어 도움을 받았다.  
Reference: <https://www.geeksforgeeks.org/count-ways-reach-nth-stair/>

The person can reach nth stair from either (n-1)th stair or from (n-2)th stair.
```
ways(n) = ways(n-1) + ways(n-2)
```

<br>

### Third solution: using dynamic programming (efficient approach)
```cpp
class Solution {
public:
    int climbStairs(int n) {
        int arr[n+1];
        arr[0]=1;
        arr[1]=1;

        for (int i=2; i<=n; i++) {
            arr[i]=0;
            arr[i] += arr[i-1];
            arr[i] += arr[i-2];
        }
        return arr[n];
    }
};
```
두 번째 솔루션의 recursive function을 dynamic programming 형식으로 푼거다.  

Runtime: 0 ms  
Memory usage: 6 MB (상위 40%)  
Time complexity: O(n);  





