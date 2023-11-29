---
title: LeetCode 191. Number of 1 Bits
lang: en
date: 2023-11-29 23:59:35
tags:
    - LeetCode
    - Bitwise operations
    - Algorithm
categories:
    - LeetCode
---

#  191. Number of 1 Bits

## Intuition

- Check how many 1 bits are there in the binary representation of `n`.
- Using the right shift operation, check whether the last bit of `n` is 1 (by checking whether `n` is odd).

## Approach
1. Initialise `ans` to 0.
2. While `n` is greater than 0 (i.e., the binary representation contains at least one 1 bit):
   1. Increase `ans` if the last bit of `n` is odd (i.e., the binary representation of n is 1).

Pseudocode of `hammingWeight()`:

```
hammingWeight(n):
	Input n a 32-bit unsigned integer
	Output number of 1 bits in the binary representation of n
	
	ans = 0
	while n > 0:
		ans += (n % 2)
		right shift n
	end while
	return ans
```

## Complexity
- Time complexity: $O(logn)$.
  - $logn$ iterations to calculate how many 1 bits are in the binary representation.

- Space complexity: $O(1)$.

## Code
```c++
class Solution {
public:
  int hammingWeight(uint32_t n) {
    int ans = 0;
    while (n > 0) {
      ans += (n % 2);
      n >>= 1;
    }
    return ans;
  }
};
```
