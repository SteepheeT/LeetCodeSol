# Problem 278 - First Bad Version - Easy
You are a product manager and currently leading a team to develop a new product. Unfortunately, the latest version of your product fails the quality check. Since each version is developed based on the previous version, all the versions after a bad version are also bad.

Suppose you have `n` versions `[1, 2, ..., n]` and you want to find out the first bad one, which causes all the following ones to be bad.

You are given an API `bool isBadVersion(version)` which returns *whether `version` is bad*. Implement a function to find the first bad version. You should minimize the number of calls to the API.

 

**Example 1:**
```
Input: n = 5, bad = 4
Output: 4
Explanation:
call isBadVersion(3) -> false
call isBadVersion(5) -> true
call isBadVersion(4) -> true
Then 4 is the first bad version.
```
**Example 2:**
```
Input: n = 1, bad = 1
Output: 1
``` 

**Constraints:**

- `1 <= bad <= n <= 2^31 - 1`

---
## Solution - C++
### 0 ms, 6 mb
- Binary Search Strategy, but instead of found a specific number, this time we found the latest good version
- This is similar to binary search, expect we need to narrow down to one element left to check is it good or bad
- If the last element is good, then we update `latest_good` and thus the next one is definitly bad
- If the last one is bad, then our last iteration has already updated `latest_good` to the previous index of this element

```
int firstBadVersion(int n) {
    int low = 1, high = n;
    int latest_good = 0;
    while(high >= low){
        int idx = low + (high - low) / 2;
        if(isBadVersion(idx)){
            high = idx - 1;
        }
        else{
            latest_good = idx;
            low = idx + 1;
        }
    }
    return latest_good + 1;
}
```