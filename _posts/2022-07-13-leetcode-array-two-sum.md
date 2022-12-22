---
title:  "(Leetcode) [Array]: Two sum"
excerpt: "solution for a leetcode array question"

categories:
  - leetcode
tags:
  - [leetcode, array, C++]

permalink: /leetcode/leetcode_array_two_sum/

toc: true
toc_sticky: true
 
date: 2022-07-13
last_modified_at: 2022-07-13
---
Topic: Array  
Difficulty: Easy


---
이 문제를 풀기 전에 학교에서 C++을 배울땐 벡터를 배우지 않았기 때문에 geeksforgeeks에서 벡터에 대해서 공부를 조금 했다.

문제의 내용은 합이 target이 되는 두 개의 element의 index들을 찾는 것이다.
중첩된 두 개의 for loop (Brute Force method)를 쓰지 않고 할 수 있는 방법을 쉽게 생각해내지 못 했다.
참고로 Brute Force의 time complexity는 O(n^2).

결국 구글에 algorithm for two sum을 검색해서 time complexity가 O(n)인, 하나의 for loop을 써서 풀 수 있는 알고리즘을 찾아 보았다.


### Solution

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> result;
        unordered_map<int, int> hash;
        
        for (int i=0; i<nums.size(); i++) {
            int temp = target - nums[i];
            
            if (hash.find(temp) != hash.end()) {
                result.push_back(i);
                result.push_back(hash[temp]);
                return result;
            }
            hash[nums[i]] = i;
        }
        return {};
    }
};
```


일반 벡터가 아닌 unordered_map이라는 컨테이너를 사용했다.
unordered_map은 key와 value로 이루어진 hash map이다.
위에 문제풀이와 같이 key와 value를 지정할 수 있다.
unordered_map을 사용하려면 헤더에 `<unordered_map>`을 명시해줘야 한다.

`find(value)` for vector / `find(key)` for unordered_map: returns an iterator to the first element in the range [first, last) that compares equal to value .
If no such element is found, it returns last element.
