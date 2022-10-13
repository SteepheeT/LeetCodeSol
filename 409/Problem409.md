# Problemm 409 - Longest Palindrome
Given a string `s` which consists of lowercase or uppercase letters, return *the length of the **longest palindrome*** that can be built with those letters.

Letters are **case sensitive**, for example, `"Aa"` is not considered a palindrome here.

 

**Example 1:**
```
Input: s = "abccccdd"
Output: 7
Explanation: One longest palindrome that can be built is "dccaccd", whose length is 7.
```
**Example 2:**
```
Input: s = "a"
Output: 1
Explanation: The longest palindrome that can be built is "a", whose length is 1.
``` 
**Constraints:**

- `1 <= s.length <= 2000`
- `s` consists of lowercase **and/or** uppercase English letters only.

---
## Solution - C++
### 10 ms, 6.7 mb
```
int longestPalindrome(string s) {
    if(s.length() == 1){
        return 1;
    }
    unordered_map<char, int> mp;
    bool single = false;
    int res = 0;
    for(int i = 0; i < s.length(); i++){
        if(!mp[s.at(i)]){
            mp[s.at(i)] = 1;
        }
        else{
            mp[s.at(i)]++;
        }
    }
    
    for(auto i : mp){
        if(i.second % 2 == 1){
            i.second--;
            single = true;
        }
            res += i.second;
    }
    res += single ? 1 : 0;
    return res;
}
```
