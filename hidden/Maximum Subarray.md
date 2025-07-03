---
share: "true"
---

# Maximum Subarray

Date: August 13, 2021 10:30 AM
Difficulty: Easy
Status: Done

We will never start or end with a non positive integer as that does not benefit us.

This is true for a non-positive range as well.

eg: in [5, -2, -4, 100, .....], there is no need to consider the [5, -2, -4] part because the sum if that range is 0. It means that if we include this area, then it will only drag the net sum downwards.

We will begin at the left of the array.

Since we do not need to return the range, we only will track the sum. If the total goes down below 0, then we will discard the previous part. Otherwise we will keep considering this range.

We will track a `globalMaxSum` which is the max of the sum of the current range in consideration (`currentSum`). This way we will consider the ranges in `O(len(nums))` and track the largest range we found till date in the global.

```python
class Solution:
    def testSol(self, nums: List[int]) -> int:

        globalMaxSum = float('-inf')
        currentSum = 0

        for num in nums:
            currentSum += num
            if currentSum > globalMaxSum:
                globalMaxSum = currentSum

            if currentSum < 0:
                currentSum = 0
        return globalMaxSum

    def maxSubArray(self, nums: List[int]) -> int:
        return self.testSol(nums)
```
