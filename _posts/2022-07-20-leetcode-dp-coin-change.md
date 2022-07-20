---
title:  "(Leetcode) [Dynamic programming]: Coin change"
excerpt: "find minimum number of coins that make a given value"

categories:
  - algorithm
tags:
  - [leetcode, dynamic programming, recursion, C++]

permalink: /algorithm/leetcode_dp_coin_change/

toc: true
toc_sticky: true
 
date: 2022-07-20
last_modified_at: 2022-07-20
---

Topic: Dynamic programming  
Difficulty: Medium

### Question

Given an integer array `coins` and an integer `amount`, return the fewest number of coins that you need to make up that amount.  
If that amount of money cannot be made up by any combination of the coins, return -1.

도저히 답을 생각해낼 수 없었다. geeksforgeeks에서 해답을 얻었다.

<br>

### First solution: recursion
```cpp
#include <iostream>
#include <vector>

using namespace std;

int coinChange(vector<int>& coins, int amount) {
    // base case
    if (amount==0) return 0;

    // initialize result
    int result = INT_MAX;

    // try every coin that has smaller value than amount
    vector<int>::iterator p;
    for (p=coins.begin(); p != coins.end(); p++) {
        if (*p <= amount) {
            int sub_result = coinChange(coins, amount-*p);

            // Check for INT_MAX to avoid overflow
            // && see if result can be minimized
            if (sub_result != INT_MAX && sub_result+1 < result)
                result = sub_result+1;
            
            if (sub_result == -1) {
                return -1;
            }
        }
    }
    if (result == INT_MAX) 
        return -1;
    return result;
}
```

하지만 recursion은 time complexity가 exponential이기 때문에 leetcode 사이트에 제출을 하면 시간 초과라고 뜬다.  
recursion tree를 그려보면 여러개의 하위 케이스 (subproblem)들이 뜬다.  
e.g. amount=11 -> 6+5 / 6+1+1+1+1+1 / ...  
이 제약점을 해결해줄 것은 dynamic programming이다.

<br>

### Second solution: Dynamic programming

```cpp
int coinChange(vector<int>& coins, int amount) {
    // table[i] for storing the minimum number of coins to get the amount i
    int table[amount+1];

    // base case
    table[0]=0;

    // initialize all table values as infinite
    for (int i=1; i<=amount; i++)
        table[i] = INT_MAX;
    
    // compute minimum coins required for all values from 1 to V.
    vector<int>::iterator p;
    for (int i=1; i<=amount; i++) {
        for (p=coins.begin(); p != coins.end(); p++) {
            if (*p <= i) {
                int sub_result = table[i-*p];
                // check whether the sub_result can be made with given coins
                // && see if results can be minimized.
                if (sub_result != INT_MAX && sub_result+1 < table[i]) {
                    table[i]=sub_result+1;
                }
            }
        }
    }

    if (table[amount] == INT_MAX)
        return -1;
    
    return table[amount];
}
```

<br>

예전부터 느낀거지만 recursion 머리는 돌아가지 않는다. 조금 더 노력해보자.


### Reference
<https://www.geeksforgeeks.org/find-minimum-number-of-coins-that-make-a-change/>