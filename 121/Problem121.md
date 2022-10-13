# Problem 121 - Best Time to Buy and Sell Stock - Easy
You are given an array `prices` where `prices[i]` is the price of a given stock on the `i^th^` day.

You want to maximize your profit by choosing a **single day** to buy one stock and choosing a **different day in the future** to sell that stock.

Return *the maximum profit you can achieve from this transaction*. If you cannot achieve any profit, return `0`.

 

**Example 1:**
```
Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.
```
**Example 2:**
```
Input: prices = [7,6,4,3,1]
Output: 0
Explanation: In this case, no transactions are done and the max profit = 0.
```

**Constraints:**

- 1 <= prices.length <= 105
- 0 <= prices[i] <= 104

---
## Solution - C++
- Greedy algorithm, select the best choice within each step

### 185 ms, 93.4 mb
```
int maxProfit(vector<int>& prices) {
    if(prices.size() <= 1){
        return 0;
    }
    int low = prices[0], high = prices[0];
    int profit = 0;
    for(int i = 0; i < prices.size(); i++){
        if(prices[i] < low){
            low = prices[i];
            high = prices[i];
        }
        else if(prices[i] > high){
            high = prices[i];
            if(high - low > profit){
                profit = high - low;
            }
        }
    }
    return profit;
}
```

### 125 ms, 93.4 mb
```
int maxProfit(vector<int>& prices) {
    if(prices.size() <= 1){
        return 0;
    }
    int low = prices[0];
    int profit = 0;
    for(int i = 0; i < prices.size(); i++){
        if(prices[i] < low){
            low = prices[i];
        }
        else if(prices[i] - low > profit){
            profit = prices[i] - low;
        }
    }
    return profit;
}
```