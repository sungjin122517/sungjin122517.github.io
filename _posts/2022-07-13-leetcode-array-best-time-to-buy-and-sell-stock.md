---
title:  "(Leetcode) [Array]: Best time to buy and sell stock"
excerpt: "solution for a leetcode array question"

categories:
  - leetcode
tags:
  - [leetcode, array, C++]

permalink: /leetcode/leetcode_array_best_time_to_buy_and_sell_stock/

toc: true
toc_sticky: true
 
date: 2022-07-13
last_modified_at: 2022-07-13
---
Topic: Array  
Difficulty: Easy


---
Vector에 주식 금액이 날짜순으로 나열되어 있다.  
거래를 해서 낼 수 있는 가장 큰 이익을 찾는 문제이다.  

By default, map is sorted in increasing order based on its key.

### My first idea
1. for loop을 이용해서 첫번째 숫자부터 각 숫자를 기준으로 둔다. max라는 int variable을 만든다.
2. 기준 숫자보다 뒤에 있는 숫자들중에 최댓값을 찾는다.
3. '최댓값-기준'이 max보다 작으면 max = 최댓값 - 기준.

결과: time-limit exceeded.





### My second idea
1. `min_element` 함수를 이용해서 제일 작은 숫자의 인덱스를 찾는다.
2. 그 인덱스 이후에 숫자들 중에서 제을 큰 숫자를 찾아서 이익을 찾는다. 
    
문제점: 이렇게 찾은 이익이 항상 최댓값이라는 보장은 없다. 무조건 최솟값으로 최대 이익을 내는건 아니기 때문이다.  
아래는 엣지 케이스이다.

![stock-question-edge-case.png](/assets/images/posts_img/stock-question-edge-case.png)





### Solution
```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int minPrice = prices[0];
        int maxProfit = 0;

        for (int i=1; i<prices.size(); i++) {
            if (minPrice > prices[i]) {
                minPrice = prices[i];
            }
            else if (maxProfit < prices[i]-minPrice) {
                maxProfit = prices[i]-minPrice;
            }
        }
        return maxProfit;
    }
};
```

굉장히 간단한 문제였다,,  
loop을 한 번만 돌고도 찾을 수 있었다.  
일단 2개의 변수, minPrice와 maxProfit을 만든다.  
loop을 돌면서 minPrice와 maxProfit을 동시에 업데이트 해주면 된다.  
minPrice는 return되지 않는 값이기 때문에 그냥 비교 용도로만 사용될 수 있다.   



아직 난 갈 길이 멀었다.