---
title: LeetCode 1930. Unique Length-3 Palindromic Subsequences
date: 2023-11-15 19:49:41
lang: en
tags:
    - LeetCode
    - Algorithm
    - Set
Categories:
    - LeetCode
---

## Intuition
- Find the first and last occurrence (say `firstOccurrence` and `lastOccurrence`) of an unused character `c`.
- Count the number of unique characters between `firstOccurrence` and `lastOccurrence` (including `c` itself).

## Approach

1. Create an empty set `visited`.
2. For every character `c` in `s`:
   1. If `c` is a member of `visited`, jump to the next character.
   2. Otherwise, find the `firstOccurrence` and `lastOccurrence` of `c` in `s`.
   3. Create an empty set `unique`.
   4. Add every character between `firstOccurrence` and `lastOccurrence` to `unique`.
   5. Add the size of `unique` to answer.

Pseudocode of `countPalindromicSubsequence`:

```
countPalindromicSubsequence(s):
	Input string s
	Output number of unique palindromic subsequences in s of length 3
	
	visited = empty set
	ans = 0
	for every character c in s:
		if c in set:
			continue
		end if
		add c to visited
		firstOccurrence = -1
		lastOccurrence = -1
		for every i from 0 to s.length():
			if firstOccurrence == -1:
				firstOccurrence = i	// Ensure that firstOccurrence only updates once
			end if
			lastOccurrence = i
		end for
		unique = empty set
		for every i from firstOccurrence + 1 to lastOccurrence:
			add s[i] to unique
		end for
		ans += unique.size()
	end for
	return ans
```

## Complexity
- Time complexity: $O(n)$.
  - At most $\Sigma = 26$ iterations of outer loop.
  - In each iteration:
    - Find `firstOccurrence` and `lastOccurence` is $O(n)$.
    - Create `unique` set is $O(n)$.
  - Overall complexity is $O(\Sigma n) = O(n)$.
- Space complexity: $O(\Sigma)$.
  - `s` only contains lowercase English letters, so $\Sigma = 26$.
  - As a consequence, the maximum size of  `visited` and `unique` is 26.

## Code
```c++
class Solution {
public:
    int countPalindromicSubsequence(string s) {
        int ans = 0;
        unordered_set<char> visited;
        for (char c : s) {
          if (visited.find(c) != visited.end()) {
            continue;
          }
          visited.insert(c);
          // Find the first and last occurence of c
          int lastOccurrence = -1;
          int firstOccurrence = -1;
          for (int j = 0; j < s.length(); j++) {
            if (s[j] == c) {
              if (firstOccurrence == -1) {
                // firstOccurence can only be updated once
                firstOccurrence = j;
              }
              lastOccurrence = j;
            }
          }
          // Count the number of unique characters between i and lastOccurance
          unordered_set<char> unique;
          for (int j = firstOccurrence+1; j < lastOccurrence; j++) {
            unique.insert(s[j]);
          }
          ans += unique.size();
        }
        return ans;
    }
};
```
