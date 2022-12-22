---
title:  "(Leetcode) [String] Longest substring without repeating characters"
excerpt: "Given a string s, find the length of the longest substring without repeating characters."

categories:
  - leetcode
tags:
  - [leetcode, string, C++]

permalink: /leetcode/leetcode-string-longest-substring-without-repeating-chars/

toc: true
toc_sticky: true
 
date: 2022-08-27
last_modified_at: 2022-08-27
---

Topic: String  
Difficulty: Medium

---

### Question
Given a string s, find the length of the longest substring without repeating characters.  
제목 그대로 문자열 내에서 반복되는 알파벳이 없는 가장 긴 부분 문자열을 찾는 문제이다.

<br>

### My first solution: time complexity O(n^2)
문자열에 첫 알파벳을 기준점으로 잡는다. 그리고 두번째 알파벳부터 시작해서 차례대로 unordered_set에 저장을 한다. 하나의 정수 variable (int max)을 세워서 for loop이 하나 돌 때마다 증가시킨다.  
이때, 반복되는 알파벳이 나오면 다음 기준 알파벳으로 넘어간다. 이런식으로 가장 큰 max를 리턴한다.  
두 개의 for loop이 사용되었기 때문에 time complexity는 O(n^2)이다.  
세트와 맵이라는 자료구조를 배움으로써 조금 더 쉽게 implement 할 수 있는 알고리즘 구현 방법들이 생긴다.  

```cpp
int lengthOfLongestSubstring(string s) {
    if (s.length()==0)
        return 0;

    int max = -1;
    int num = 0;
    for (int i=0; i<s.length(); i++) {
        unordered_set<char> set;
        num = 0;
        // vector<bool> set(26);   // default values in set are false
        for (int j=i; j<s.length(); j++) {
            // if (set[s[j]-'a'])
            //     break;
            // set[s[j]-'a']=true;
            if (set.find(s[j]) != set.end())
                break;
            set.insert(s[j]);
            num++;
        }
        cout << num << endl;
        if (max<num)
            max = num;
    }
    return max;
}
```

runtime이 어마무시하다.  
![runtime-longest-substring-without-repeating-characters.png](/assets/images/posts_img/algorithm/runtime-longest-substring-without-repeating-characters.png)

<br>

### Second solution: time complexity O(n)
두번째 방법은 이미 거쳐간 알파벳의 index를 lastIndex라는 배열에 저장함으로써 linear time complexity를 가능케 했다.  
int i를 starting index로 두고, int result라는 변수에 최대 길이를 저장한다.  
for loop 안에서,
1. **first line**: 만약 반복되는 알파벳이 나오면, i에 1을 증가시킨다.
2. **second line**: 만약 현재 i에서 j까지의 길이가 제일 길면, result에 업데이트 시킨다.
3. **third line**: 매번 특정 알파벳이 마지막으로 나타나는 index를 업데이트 시킨다. 

이런 발상은 대체 어떻게 하는 걸까. 대단하다. 

```cpp
int lengthOfLongestSubstring(string s) {
    int result = 0;

    // last index of all characters is initialized as -1
    vector<int> lastIndex(256, -1); // number of chars = 256

    int i = 0;  // start of window
    for (int j=0; j<s.length(); j++) {
        i = max(i, lastIndex[s[j]+1]);

        // update result if we get a larger window
        result = max(result, j-i+1);

        // update last index of j
        lastIndex[s[j]] = j;
    }
    return result;
}
```

<br>

### Summary
이 문제에서의 관건은 모든 알파벳을 기준점으로 두어서 가장 길게 나오는 부분 문자열을 찾을때 얼마나 효율적으로 찾을수 있는지 이다.  
첫번째 방법은 직관적이지만 두 개의 for loop이 사용되어서 time complexity가 O(n^2)이다. 비효율적인 편이다.  
두번째 방법은 array를 이용해서 반복되는 알파벳의 index를 저장해서 기준점을 계속 이동시키기 때문에 하나의 루프만으로 구현할 수 있다.  

기억하자. 반복되는 알파벳의 index를 저장해서 하나의 루프로 효율성을 증가.

<br>

### References
<https://www.geeksforgeeks.org/length-of-the-longest-substring-without-repeating-characters/>