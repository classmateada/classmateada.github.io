---
title: LeetCode 1846. Maximum Element After Decreasing and Rearranging
date: 2023-11-15 19:47:57
lang: en
tags:
    - LeetCode
    - Algorithm
    - Sorting
categories:
    - LeetCode
---

## Intuition
- Set the first element `arr[0]` to 1.
- Limit the difference of two adjacent elements to 1 or less than 1, which means `arr[i+1]` is the same as `arr[i]` or equal to `arr[i] + 1`.
- Return the maximum possible value in `arr`.

## Approach
1. Set `arr[0]` to 1 (that's the rule of this challenge).
2. Set `max` to 1, which represents the maximum possible value in arr is 1.
3. Sort `arr` in ascending order.
4. Iterate over `arr` from the second element `arr[1]` (because `arr[0]` has already been set to 1):
   1. Set `arr[i]` to `max` if it's the same as or higher than `max`, then increase `max` by 1.
   2. Do nothing if `arr[i]` is smaller than `max` (which couldn't happen because `arr` has already been sorted in ascending order).

5. Return `max`.

Pseudocode of `maximumElementAfterDecrementingAndRearranging`:

```
maximumElementAfterDecrementingAndRearranging(arr):
	Input arr an array of integers
	Output maximum possible element in arr after decrementing and rearranging
	
	sort arr in ascending order
	max = 0
	arr[0] = 1
	for every i from 0 to arr.size():
		if arr[i] >= max + 1:
			arr[i] = max
			max++
		end if
	end for
	return max
```

## Complexity
- Time complexity: $O(nlogn)$.
  - Sorting `arr` in ascending order is $O(nlogn)$.
  - Iterate over `arr` to update `arr` and `max` is $O(n)$.
  - Overall complexity is $O(nlogn)$.
  - $n$ is the total size of `arr`.

- Space complexity: $O(1)$.

## Code
```c++
class Solution {
public:
    int maximumElementAfterDecrementingAndRearranging(vector<int>& arr) {
      sort(arr.begin(), arr.end());
      int max = 1;
      arr[0] = 1;
      for (int i = 1; i < arr.size(); i++) {
        if (arr[i] >= max + 1) {
          arr[i] = max;
          max++;
        }
      }
      return max;
    }
};
```
