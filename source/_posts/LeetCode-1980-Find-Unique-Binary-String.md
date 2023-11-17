---
title: LeetCode 1980. Find Unique Binary String
lang: en
date: 2023-11-17 20:33:59
tags:
  - LeetCode
  - Algorithm
  - Recursion
categories:
  - LeetCode
---

# Approach 1: Recursive

## Intuition
- Since the maximum possible length of `nums` is $2^{16} = 65536$, which is not so big. As a consequence, it's possible to solve this problem recursively.
- During the recursion, we can either choose from adding a zero `"0"` or adding a one `"1"` to the string.
- Try generating a unique string of length 

## Approach
1. Convert `nums` to a set `unique`.
2. Try generating a string from an empty string `s`:
   1. Try adding a zero (`"0"`) to the end of `s`.
   2. If adding a zero is not possible (i.e., the string after adding a zero is a member of `unique`), try adding a one (`"1"`).
   3. If the length of `s` euqals to `nums.size()` and `s` is not a member of `unique`, then return `s`.
   4. Otherwise, return an empty string.

Pseudocode of this approach:

```
generate(s, maxLen, unique):
	Input s a string of length l
		maxLen the maximum length of s
		unique a set that contains all unique strings that can't be used
	Output a unique string of length maxLen
	
	if len(s) == maxLen:
		if s is not a member of unqiue:
			return s
		else:
			return empty string
		end if
	end if
	
	zero = generate(s + "0", maxLen, unique)
	if zero is not an empty string:
		return zero
	else:
		return generate(s + "1", maxLen, unique)
	end if

findDifferentBinaryString(nums):
	Input nums array of unique binary strings
	Output a unique binary string that not contains in nums
	
	unique = empty set
	for every string s in nums:
		add s to unique
	end for
	return generate("", nums.size(), unique)
```

## Complexity
Time complexity:

- $n$ calls to generate a unique string of length $n$.
- In each call:
  - $2$ calls to generate a unique string of length $len(s)+1$ (in the worst case).
- Overall complexity is $O(n^2)$.

Space complexity: $O(n)$.

- The set to store all unique strings uses a space of $O(n)$.
- The maximum length of the call stack will grow to a size of $O(n)$.

## Code
```c++
class Solution {
public:
  string generate(string s, int maxLen, unordered_set<string> unique) {
    if (s.size() == maxLen) {
      if (unique.find(s) == unique.end()) {
        // Return this string if it's unique
        return s;
      } else {
        // Otherwise return an empty string
        return "";
      }
    }

    // Try adding a zero to the end of s
    string zero = generate(s + "0", maxLen, unique);
    if (zero.size() > 0) {
      return zero;
    }
    // Adding a one to the end of s if it's not possible to add a zero
    return generate(s + "1", maxLen, unique);
  }

  string findDifferentBinaryString(vector<string>& nums) {
    unordered_set<string> unique;
    for (string s : nums) {
      unique.insert(s);
    }
    return generate("", nums.size(), unique);
  }
};
```

# Approach 2: Convert binary strings to decimal integers

## Intuition

- We can convert the binary strings to decimal integers and store them in a set. The binary string of any integer that is not a member of this set is the answer.

## Approach
- Convert binary strings to decimal integers and store them in a set `digits`.
- Search from 0 to $2^n$ (`n` is the size of `nums`):
  - If a number is not a member of `digits`, then convert it to a binary string and return it.

Pseudocode of this approach:

```
findDifferentBinaryString(nums):
	Input nums array of unique binary strings
	Output a unique binary string that not contains in nums
	
	digits = empty set
	for every string binary in nums:
		convert binary to decimal integer
		join this decimal integer to digits
	end for
	for all i from 0 to pow(2, nums.size()):
		if i is not a member of digits:
			convert i to a binary string
			return this binary string
		end if
	end for
	return empty string
```

## Complexity
Time complexity: $O(2^n)$.

- $n$ iterations to convert binary strings to integers and add them to the set.
- In each iteration:
  - Converting a binary string to a decimal digit is $O(n)$.
- At most $2^n$ iterations to find a decimal integer that is not a member of `digits`.
- Overall complexity is $O(n^2)$.

Space complexity: $O(n)$.

- The maximum size of `digits` is $n$.

## Code
```c++
class Solution {
public:
  string findDifferentBinaryString(vector<string>& nums) {
    unordered_set<int> digits;

    // Convert binary strings to digits
    for (string binary : nums) {
      digits.insert(bitset<16>(binary).to_ulong());
    }

    // Find the first digit that's not a member of the digigts set
    int maximumNumber = pow(2, nums.size());
    for (int i = 0; i < maximumNumber; i++) {
      if (digits.find(i) == digits.end()) {
        return bitset<16>(i).to_string().substr(16 - nums.size());
      }
    }
    return "";
  }
};
```
