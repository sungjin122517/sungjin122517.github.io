---
title:  "(Leetcode) [Binary]: Sum of two integers"
excerpt: "solution for a leetcode binary question"

categories:
  - algorithm
tags:
  - [leetcode, binary, C++]

permalink: /algorithm/leetcode_binary_sum_of_two_integers/

toc: true
toc_sticky: true
 
date: 2022-07-15
last_modified_at: 2022-07-15
---

Topic: Binary   
Difficulty: Medium

---

덧셈과 뺄셈 연산자 (+, -) 사용 없이 두 정수의 합을 구하는 문제.

일단 단원 제목이 binary여서 binary를 이용해야 한다는 것은 바로 알아차렸다.


### My first idea
1. 십진법 수를 이진법으로 변경.
2. 이진법 덧셈하기.
3. 이진법으로 쓰여있는 답을 십진법으로 다시 변경.


### 문제점
만약 답이 음수이면 음수를 절댓값 씌운 양수로 변경하는 과정이 굉장히 복잡해진다.   
이게 뭔 소리냐? 2진법에서 MSB(most significant bit)는 부호를 나타내기 때문이다 (2's complement).   
1 for negative number, and 0 for positive number.   
음수를 양수값으로 변경하려면 각 digit의 반대되는 숫자로 바꾸고 (0이면 1로, 1이면 0으로) LSB (least significant bit)에 1을 더한다.   
주저리 주저리 썼지만 결론은 이 과정으론 코드가 굉장히 길어질거고 비효율적이란 것이다.


### Solution
```cpp
class Solution {
public:
    int getSum(int a, int b) {
        while (b != 0) {
            unsigned carry = a&b;   // carry should be unsigned to deal with negative numbers
            a = a^b;    
            b = carry << 1;
        }
        return a;
    }
};
```


이번엔 geeksforgeeks에서 도움을 받았다.   
다섯줄이면 될 것을 70줄을 쓰고 앉아있었다.

1. AND operator를 이용해서 carryin을 찾는다.
2. XOR operator를 이용해서 각 digit에서 0+1=1이나 1+0=1 계산을 해준다. 0+0은 0일테고, 1+1은 carryin으로 넘어갈테니 0이 될 것이다.   

하다가 b (carryin)이 0이 되면 끝낸다.
   

e.g.   
a=0010, b=0011

carry=0010  
a=0001  
b=0100  

carry=0000  
a=0101  
b=0000  

return a=0101