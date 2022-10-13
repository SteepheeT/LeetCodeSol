# Problem 217 - Contains Duplicate - Easy
Given an integer array `nums`, return *`true` if any value appears **at least twice** in the array*, and return *`false` if every element is distinct*.

 

**Example 1:**
```
Input: nums = [1,2,3,1]
Output: true
```

**Example 2:**
```
Input: nums = [1,2,3,4]
Output: false
```

**Example 3:**
```
Input: nums = [1,1,1,3,3,4,3,2,4,2]
Output: true
``` 

**Constraints:**

- `1 <= nums.length <= 10^5`
- `-10^9 <= nums[i] <= 10^9`

---
## Solution - C++
### 93 ms, 51.5 mb
- Map the vector value as a key to a map
- If there's already a value there, then return true; if all values got mapped and no dulicate found, then return false
```
bool containsDuplicate(vector<int>& nums) {
    if(nums.size() == 1){
        return false;
    }
    
    unordered_map<int, bool> mp;
    for(int i=0; i<nums.size(); i++){
        if(mp[nums[i]] == true){
            return true;
        }
        else{
            mp[nums[i]] = true;
        }
    }
    return false;
}
```