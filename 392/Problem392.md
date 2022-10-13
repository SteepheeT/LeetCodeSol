# Problem 392 - Is Subsequence - Easy
Given two strings `s` and `t`, return `true` if `s` is a ***subsequence*** of `t`, or `false` otherwise.

A subsequence of a string is a new string that is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (i.e., `"ace"` is a subsequence of `"abcde"` while `"aec"` is not).

 

Example 1:
```
Input: s = "abc", t = "ahbgdc"
Output: true
```
Example 2:
```
Input: s = "axc", t = "ahbgdc"
Output: false
```

Constraints:
```
0 <= s.length <= 100
0 <= t.length <= 104
s and t consist only of lowercase English letters.
```

**Follow up:** Suppose there are lots of incoming s, say s1, s2, ..., sk where k >= 109, and you want to check one by one to see if t has its subsequence. In this scenario, how would you change your code?

---
## Solution - C++
###  4 ms, 6.7mb
```
bool isSubsequence(string s, string t) {
    if(s.length() == 0){
        return true;
    }
    for(int i = 0; i < s.length(); i++){
        size_t pos = t.find(s[i]);
        if(pos == string::npos){
            return false;
        }
        t = t.substr(pos + 1);
    }
    return true;
}
```
### 0 ms, 6.4mb
```
bool isSubsequence(string s, string t) {
    int s_len = s.length(), t_len = t.length();
    int j = 0;
    for(int i = 0; i < t_len; i++){
        if(t[i] == s[j]){
            j++;
        }
    }
    return (j == s_len);
}
```
---
## Solution - Java
