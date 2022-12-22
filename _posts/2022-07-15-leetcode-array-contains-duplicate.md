---
title:  "(Leetcode) [Array]: Contains duplicate"
excerpt: "solution for a leetcode array question"

categories:
  - leetcode
tags:
  - [leetcode, array, C++]

permalink: /leetcode/leetcode_array_contains_duplicate/

toc: true
toc_sticky: true
 
date: 2022-07-15
last_modified_at: 2022-07-15
---


Topic: Array  
Difficulty: Easy  

Array element 중에 하나라도 중복되는 게 있으면 return true; else return false.

### Solution
```cpp
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        vector<int> temp;

        for (int i=0; i<nums.size(); i++) {
            if (find(temp.begin(), temp.end(), nums[i]) != temp.end())
                return true;
            temp.push_back(nums[i]);
        }
        return false;
    }
};
```


첫 번째로 풀었던 문제 (two sum)을 인용해서 풀었다.  
for loop을 이용해서 temp라는 임의의 벡터에 숫자를 하나씩 넣는데, 넣기 전에 temp 안에 넣으려는 숫자와 같은 숫자가 있으면 return true.  
없으면 temp에 저장하고 loop 계속 반복.

결과:   
runtime은 상위 95퍼이다 (2941 ms); 더 효율적인 방법이 있나보다.  
memory는 상위 30퍼 (47.4 MB). 나름 선방한듯?


---
여러가지의 답안이 있었다. 그 중 세 개를 소개한다.

### 1. Use of set (unordered_set)
고유한 요소만 유지하는 배열에서 집합을 구성한다. 그런 다음 집합의 크기를 배열의 길이와 비교한다.  
둘의 크기가 같으면 중복 없음, 다르면 중복 있음.

```cpp
bool containsDuplicate(vector<int>& nums) {
    unordered_set<int> temp(nums.begin(), nums.end());

    if (temp.size() == nums.size())
        return false;
    else
        return true;
}
```

결과: runtime은 10배 이상 빨라짐 (211 ms = 상위 89퍼). 대신 메모리 사용은 증가 (55.3MB = 상위 94퍼)


### 2. Use of sort
배열을 정렬하고 연속 요소의 각 쌍을 비교하여 중복을 확인한다.  
Time complexity: O(nlog(n)).

```cpp
bool containsDuplicate(vector<int>& nums) {
    sort(nums.begin(), nums.end());
    for (int i=0; i<nums.size()-1; i++) {
        if (nums[i]==nums[i+1])
            return true;
    }
    return false;
}
```

결과: runtime 149 ms (상위 53퍼), 메모리 사용 46.6 MB (상위 20퍼).


### 3. Use of adjacent_find
`std::adjacent_find`: 정렬된 배열에서 동일한 인접 요소의 첫 번째 발생을 찾는다.  
중복이 있으면 첫 번째 중복 요소의 반복자를 반환한다. 없으면 범위 끝을 반환한다.  

```cpp
bool containsDuplicate(vector<int>& nums) {
    sort(nums.begin(), nums.end());
    
    if (adjacent_find(nums.begin(), nums.end()) != nums.end())
        return true;
    else 
        return false;
}
```

결과: runtime 114 ms (상위 20퍼), 메모리 사용 46.7 MB (상위 20퍼).