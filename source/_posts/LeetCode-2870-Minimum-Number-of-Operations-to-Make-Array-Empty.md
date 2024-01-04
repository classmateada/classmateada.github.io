---
title: LeetCode 2870. Minimum Number of Operations to Make Array Empty
lang: en
date: 2024-01-04 21:40:46
tags:
    - Algorithm
    - LeetCode
    - Mathematics
categories:
    - LeetCode
---

## Intuition

- Mathematics problem.
- Count the number of occurrences for all numbers in `nums`.
- Specify the operation based on the number of occurrences.

## Approach

The number of operations required to remove a specific number of occurrences can be found as follows:

| Number of Occurrences | Number of Operations to Remove this Number |
| --------------------- | ------------------------------------------ |
| 1                     | -1 (no solution)                           |
| 2 / 3                 | 1                                          |
| 4 / 5 / 6             | 2                                          |
| 7 / 8 / 9             | 3                                          |
| 10 / 11 / 12          | 4                                          |
| ...                   | ...                                        |
| n-2 / n-1 / n         | $\lceil n/3 \rceil$                        |

1. Create an empty map `count`.
2. Initialise `ans` to 0.
3. Count the number of occurrences for every number in `nums`, and store it in `count`.
4. Use the table above to calculate the number of operations needed.
5. Return `ans`.

Pseudocode of `minOperations()`:

```
minOperations():
	Input nums an array of integers
	Output minimum number of operations to make array empty
	
	count = empty map
	ans = 0
	for all num in nums do
		if num not in count then
			count[num] = 1
		else
			count[num] += 1
		end if
	end for
	for all (key, value) in map do
		if value == 1 then
			return -1
		end if
		ans += celi(value / 3)
	end for
```

## Complexity
Time complexity: $O(n)$.

- $n$ iterations to count the number of occurances in the array.

Space complexity: $O(n)$.

- `count` will take a space of $n$ if all the numbers in the array are unique.

## Code
```c++
class Solution {
public:
  int minOperations(vector<int>& nums) {
    unordered_map<int, int> count;
    for (int num : nums) {
      if (count.find(num) == count.end()) {
        count[num] = 1;
      } else {
        count[num]++;
      }
    }
    int ans = 0;
    for (auto it = count.begin(); it != count.end(); it++) {
      if (it->second == 1) {
        return -1;
      }
      ans += ceil((double)(it->second) / 3);
    }
    return ans;
  }
};
```
