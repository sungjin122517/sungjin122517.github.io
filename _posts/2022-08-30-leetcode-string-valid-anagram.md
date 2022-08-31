---
title:  "(Leetcode) [String] Valid anagram"
excerpt: "Determine whether a string is an anagram of another string"

categories:
  - algorithm
tags:
  - [leetcode, string, C++]

permalink: /algorithm/leetcode-string-valid-anagram/

toc: true
toc_sticky: true
 
date: 2022-08-30
last_modified_at: 2022-08-30
---

Topic: String  
Difficulty: Easy

---

### Question
Given two strings `s` and `t`, return true if `t` is an **anagram** of `s`, and `false` otherwise.  
**anagram**: a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

<br>

### Solution
10분도 안 걸려서 풀었다. 이런 날이 오다니.  

Anagram이란 알파벳의 종류와 갯수는 똑같지만 순서가 서로 다른 단어를 뜻하는 단어이다. 두 개의 문자열이 anagram인지 확인하려면 모든 알파벳의 종류가 겹치는지, 또 각 알파벳의 갯수가 같은지를 확인하면 된다.  
1. 일단 문자열의 길이가 다르면 절대 anagram이 될 수 없으므로 첫번째 줄에서 문자열의 길이를 확인해줬다.
2. 크기가 26인 두 개의 배열을 형성해서 각 알파벳의 갯수를 표시했다. 문자열에서 각 알파벳에 `a`를 빼줌으로써 a의 index=0, b의 index=1, ... , z의 index=26이 된다.
3. 루프를 돌려서 두 배열의 element가 모두 같은지 확인하여 완전히 같으면 true, 아니면 false를 리턴한다.

```cpp
bool isAnagram(string s, string t) {
    if (s.length() != t.length())
        return false;

    int arr1[26] = { };
    int arr2[26] = { };

    for (int i=0; i<s.length(); i++) {
        arr1[s[i]-'a']++;
        arr2[t[i]-'a']++;
    }

    for (int j=0; j<26; j++) {
        if (arr1[j] != arr2[j])
            return false;
    }

    return true;
}
```

<br>

오늘은 레퍼런스 없음~!
