---
title:  "(Leetcode) [String] Longest repeating character replacement"
excerpt: "Given a string s and integer k, find the maximum length substring having all same characters after k changes."

categories:
  - leetcode
tags:
  - [leetcode, string, C++, window slicing]

permalink: /leetcode/leetcode-string-longest-repeating-character-replacement/

toc: true
toc_sticky: true
 
date: 2022-08-29
last_modified_at: 2022-08-29
---

Topic: String  
Difficulty: Medium

---

### Question
Given a string `s` and an integer `k`, you can choose any character of the string and change it to any other uppercase English character at most k times.  
Return the length of the longest substring containing the same lteer you can get after perfoming the above operations.

주어진 문자열에서, 알파벳 k개를 제일 긴 부분 문자열이 나오게끔 바꿔서 그의 길이를 리턴해라.

<br>

### Solution: Window slicing method
전혀 감이 오지 않아서 geeksforgeeks와 유튜브를 찾아보았다.  
Window sliding method를 사용했다.  
arr 배열은 window 안에 있는 특정 글자의 갯수를 나타내기 위함이다. 그래서 배열의 크기는 알파벳의 총 개수 (26개)이다.

window의 오른쪽 index를 for loop을 이용해 늘려주는 방식으로 구현한다.  
창문 안에 있는 가장 많이 반복되는 알파벳으로 나머지 다른 알파벳을 바꿔주는게 가장 효율적으로 longest repeating substring을 가질 수 있는 방법이다.  
그래서 `int newlyAddedCharNum`에 <mark>새로이 바뀌어야 하는 알파벳의 갯수</mark>를 저장한다.  
newlyAddedCharNum (바뀌어야 하는 알파벳의 갯수)가 k보다 크면, 왼쪽 index를 한 칸 옮긴다. 그러면서 창문 밖으로 나가 떨어진 알파벳의 개수를 하나 줄인다.  

```cpp
int characterReplacement(string s, int k) {
    int result = 0;
    int leftInd = 0;
    int arr[26] = { };
    int windowSize;

    for (int j=0; j<s.length(); j++) {
        // as window enlarges, increment the number of newly added character
        arr[s[j]-'A']++;

        // saves the number of characters that needs to be changed to obtain the longest repeating substring
        int newlyAddedCharNum = j-leftInd+1 - *max_element(arr, arr+26);
        if (newlyAddedCharNum > k) {
            arr[s[leftInd]-'A']--;
            leftInd++;
        }

        result = max(result, j-leftInd+1);
    }
    return result;
}
```

![longest-repeating-character-replacement1.jpg](/assets/images/posts_img/algorithm/longest-repeating-character-replacement1.jpg)
![longest-repeating-character-replacement2.jpg](/assets/images/posts_img/algorithm/longest-repeating-character-replacement2.jpg)

<br>

### Summary
저번에도 window sliding 방법을 썼었는데 언제였지.

<br>

### References
<https://www.youtube.com/watch?v=gqXU1UyA8pk>