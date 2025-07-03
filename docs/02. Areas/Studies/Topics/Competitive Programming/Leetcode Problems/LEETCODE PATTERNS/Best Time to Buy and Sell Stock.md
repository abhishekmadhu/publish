---
share: "true"
---

# Best Time to Buy and Sell Stock

Companies: Adobe, Amazon, Apple, Bloomberg, Facebook, Goldman Sachs, Google, Intuit, Microsoft, Snapchat, Uber
Date: August 13, 2021 10:00 AM-10:20 AM
Difficulty: Easy
Review Date: September 11, 2021
Status: Done

Brute force gets TLE, so `n log(n)` is not acceptable.

When doing the review, try to solve this problem if the difference in prices is given instead of the actual prices of each day.

Also, check out the description of the problem in the CLRS book.

```python
class Solution:
    def maxProfitBruteForce(self, prices: List[int]) -> int:
				# This is the bad n log n solution. See the O(n) solution below.
        max_profit = 0
        for i in range(0, len(prices)-1):
            buy_price = prices[i]
            for j in range(i+1, len(prices)):
                sell_price = prices[j]
                profit = sell_price - buy_price
                if profit > max_profit:
                    max_profit = profit

        return max_profit


    def maxProfitRev(self, prices: List[int]) -> int:
        maxVal = prices[-1]
        maxProfit = 0
        for i in range(len(prices) - 1, -1, -1):
            if prices[i] > maxVal:
                maxVal = prices[i]

            else:
                profit = maxVal - prices[i]
                if profit > maxProfit:
                    maxProfit = profit
        return maxProfit

    def maxProfit(self, prices: List[int]) -> int:
        # return self.maxProfitBruteForce(prices)
        return self.maxProfitRev(prices)
```
