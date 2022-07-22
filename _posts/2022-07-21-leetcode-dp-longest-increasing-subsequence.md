---
title:  "(Leetcode) [Dynamic programming] Longest increasing subsequence"
excerpt: "find longest increasing subsequence of given array"

categories:
  - algorithm
tags:
  - [leetcode, dynamic programming, recursion, C++]

permalink: /algorithm/leetcode_dp_longest_increasing_subsequence/

toc: true
toc_sticky: true
 
date: 2022-07-21
last_modified_at: 2022-07-21
---

Topic: Dynamic programming  
Difficulty: Medium

### Question
Given an integer array `nums`, return the length of the longest strictly increasing subsequence.

<br>

### My first solution

```cpp
int lengthOfLIS(vector<int>& nums) {
    int len = nums.size();
    int arr[len];
    for (int i=0; i<len; i++) {
        arr[i]=0;
    }

    for (int i=0; i<len; i++) {
        if (arr[i] == 0) { arr[i]=1; }
        else { continue; }

        vector<int>::iterator p = nums.begin()+i+1;
        int p_arr = i+1;
        vector<int>::iterator mark=p-1;
        int mark_arr = p_arr-1;

        for (p; p!=nums.end(); p++) {
            if (*p > *mark) {
                if (arr[p_arr] < arr[mark_arr]+1) {
                    arr[p_arr] = arr[mark_arr]+1;
                    mark_arr = p_arr;
                    mark = p;
                }
            }
            p_arr++;
        }
    }

    return *max_element(arr, arr+len);
}
```

완벽한 알고리즘을 발견했다고 생각했지만, 이건 큰 오산이였다.

일단 longest subsequence array의 요소 갯수를 저장하기 위한 array를 하나 만들어준다 (arr[]).

첫번째 for loop은 sequential array의 시작점을 잡기 위함이고,
두번째 loop에선 iterator가 두 개 쓰인다.  
sequential array를 이어나가기 위해선 바로 전의 element와 크기 비교를 해야하기 때문이다.

비교하는 과정에서 제약점이 하나 발생한다.

```
nums = [0 1 0 3 2 3]

arr =  [1 2 1 3 2 3] -> my algorithm (wrong)
arr =  [1 2 1 1 3 4] -> correct algorithm
```

nums에서 만들 수 있는 가장 긴 subarray가 [0 1 2 3]이다.  
하지만 내 코드에서 p iterator가 순서대로 움직이기 때문에, 뒤에 더 작은 숫자가 있을수도 있는데 비교를 하지 않아서
1 다음에 2가 있음에도 불구하고 2보다 앞에 있는 3을 채택해버린다.  
그러므로 2는 무시가 되어버린다.  
그렇다면 해결방법이 무엇이 있을까??

해결 방법을 못 찾아서 결국엔 geeksforgeeks,,

<br>

### My second solution: Dynamic programming
일단 코드는 보지 않고 설명 (illustration)만 읽어봤다.

```
nums[] = {3, 10, 2, 11}
arr[] = {1, 1, 1, 1} (initialization)

1. arr[2] > arr[1] -> arr[2] = max(arr[2], arr[1]+1) = 2
2. arr[3] < arr[1] -> no change
3. arr[3] < arr[2] -> no change
4. arr[4] > arr[1] -> arr[4] = max(arr[4], arr[1]+1) = 2
5. arr[4] > arr[2] -> arr[4] = max(arr[4], arr[2]+1) = 3
6. arr[4] > arr[3] -> arr[4] = max(arr[4], arr[3]+1) = 3
```

p라는 iterator를 두고, 이중 루프를 이용해서 p 이전에 있는 모든 element들과 비교를 하게 하면 나의 첫번째 solution의 문제점이 해결이 된다.

```cpp
int lengthOfLIS(vector<int>& nums) {
    int len = nums.size();
    int arr[len];
    for (int i=0; i<len; i++) {
        arr[i]=1;
    }
    if (len==1) { return 1; }

    vector<int>::iterator p;
    int p_arr = 1;
    for (p=nums.begin()+1; p != nums.end(); p++) {
        vector<int>::iterator mark;
        int mark_arr = 0;
        for (mark=nums.begin(); mark != p; mark++) {
            if (*p > *mark) {
                if (arr[p_arr] < arr[mark_arr]+1) {
                    arr[p_arr] = arr[mark_arr]+1;
                }
            }
            mark_arr++;
        }
        p_arr++;
    }

    return *max_element(arr, arr+len);
}
```

runtime: 163 ms (상위 30%)  
memory usage: 10.4 MB (상위 30%)  
time complexity: O(n^2)  

문제 follow up에서 time complexity가 O(nlog n)인 알고리즘을 찾아보라고 했다. 난 못 찾아.

<br>

### Third solution: Lower bound based approach (time complexity of O(nlog n))

```cpp
int lengthOfLIS(vector<int>& nums) {
    vector<int> arr;
    int len = nums.size();
    for (int i=0; i<len; i++) {
        // lower_bound searches for nums[i] by binary search.
        // if nums[i] doesn't exist in arr, p의 위치는 nums[i]보다 큰 값 중에 가장 작은 값을 가르킴.
        vector<int>::iterator p = lower_bound(arr.begin(), arr.end(), nums[i]);

        // p==nums.end() if all values of arr < nums[i]
        if (p==nums.end()) { arr.push_back(nums[i]); }
        // replace *p with 자신보다 큰 값 중 가장 작은 값.
        // 따라서 arr의 길이에는 변화가 없지만, 원소가 더 작은 값으로 대체되었으므로 더 큰 값을 원소로 가즈는 부분 배열보다는 항상 이득이다.
        else { *p = nums[i]; }

        return arr.size();
    }
}
```



### Reference
<https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/>
<https://www.geeksforgeeks.org/c-program-for-longest-increasing-subsequence/>

