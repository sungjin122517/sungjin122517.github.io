---
title:  "(Leetcode) [Binary]: Counting bits"
excerpt: "count the number of bits of 1"

categories:
  - algorithm
tags:
  - [leetcode, binary, C++]

permalink: /algorithm/leetcode_binary_counting_bits/

toc: true
toc_sticky: true
 
date: 2022-07-17
last_modified_at: 2022-07-17
---

Topic: binary  
Difficulty: easy

### 문제
 Given an integer n, return an array ans of length n + 1 such that for each i (0 <= i <= n), ans[i] is the number of 1's in the binary representation of i.

<br>

---
### Solution 1

```cpp
class Solution {
public:
    vector<int> countBits(int n) {
        vector<int> arr;
        arr.push_back(0);
        if (n==0) {return arr;}
        arr.push_back(1);
        
        for (int i=2; i<n+1; i++) {
            int temp=i;
            int count=0;
            while (temp) {
                if (temp%2==1) {count++;}
                temp /= 2;
            }
            arr.push_back(count);
        }
        return arr;
        
    }
};
```

1. **Simple method**   
time complexity: O(nlogn)   
runtime: 16 ms (상위 87%)  
memory usage: 8.7 MB (상위 70%)   

<br>

### Solution 2

```cpp
class Solution {
public:
    vector<int> countBits(int n) {
        vector<int> arr(n+1, 0);

        for (int i=1; i<n+1; i++) {
            int part1 = arr[i/2];   // == arr[i>>1] (right-shift)
            int part2 = i&1;    // LSB of i

            arr[i]=part1+part2;
        }
        return arr;
        
    }
};
```

2. **Dynamic programming (dp)**  
time complexity: O(n)  
runtime: 8 ms (상위 40%)
memory usage: 7.9 MB (상위 30%)  


문제 끝에 Follow up (후속편) 부분에 time complexity가 O(n log n)인 알고리즘은 찾기 쉬우니 O(n)인 알고리즘도 찾아보라고 써 있었다.  
요즘 map에 꽂혀서 map을 이용한 방법을 생각해보다가 구글 찬스를 썼는데 dynamic programming을 이용하면 된다고 했다.  

<br>

### Dynamic programming (dp)
dp is mainly an <mark>optimization over plain recursion</mark>.  
The limitation of recursion is that it has repeated calls for some inputs. The idea of dp is to simply <mark>store the results of subproblems</mark>, so that we do not have to re-compute them when needed later. This <mark>reduces time complexities</mark> from exponential to polynomial (linear in the solution above).

<br>

### Reference
<https://www.geeksforgeeks.org/dynamic-programming/>