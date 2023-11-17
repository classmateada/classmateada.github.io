---
title: LeetCode 1877. Minimize Maximum Pair Sum in Array
lang: en
date: 2023-11-17 20:36:13
tags:
  - LeetCode
  - Algorithm
  - Sorting
categories:
  - LeetCode
---

## Intuition
- Pairing the biggest number with the smallest number leads to the minimum pair sum for the biggest number.
- Remove them from the array, find the next biggest and smallest number, and pair them.
- Find the maximum pair sum while pairing and return it after the array is empty.

## Approach
1. Sort `nums` in ascending order.
2. Initialise `ans` with 0, which represents that the maximum pair sum in `nums` is 0.
3. Iterate over `nums` from 0 to `nums.size() / 2 - 1`.
4. On each iteration:
   1. Pair `nums[i]` with `nums[nums.size()-1-i]`.
   2. Calculate their pair sum and update `ans`.
5. Return `ans`.

Pseudocode of this problem:

```
minPairSum(nums):
	Input nums array of positive integers of size n
	Output the minimized maximum pair sum
	
	sort nums in ascending order
	ans = 0
	for all i from 0 to n / 2:
		// Pair nums[i] (the minimum number) with nums[n-1-i] (the maximum number)
		ans = max(ans, nums[i] + nums[n-1-i])
	end for
	return ans
```

## Complexity
Time complexity: $O(nlogn)$.
- Sorting `nums` in ascending order is $O(nlogn)$.

- $n / 2$ iterations to pair elements and find the maximum pair sum.

- In each iteration:
  - Calculate the pair sum and update the maximum pair sum is $O(1)$.

- Overall complexity is $O(nlogn)$.

Space complexity: $O(1)$.

## Code
```c++
class Solution {
public:
  int minPairSum(vector<int>& nums) {
    sort(nums.begin(), nums.end());
    int ans = 0;
    for (int i = 0; i < nums.size() / 2; i++) {
      ans = max(ans, nums[i] + nums[nums.size()-1-i]);
    }
    return ans;
  }
};
```
