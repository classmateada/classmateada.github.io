---
title: Hard | LeetCode 2147. Number of Ways to Divide a Long Corridor
lang: en
date: 2023-11-29 23:59:59
tags:
    - LeetCode
    - LeetCode hard problems
    - Algorithm
    - Dynamic programming
categories:
    - LeetCode
---

## Intuition

- Dynamic programming (bottom-up approach).
- Based on hint 1 (divide the corridor into segments):
  - There will be no solution if the number of seats is odd.
  - Divide `corridor` into multiple groups; each group contains **exactly** two seats and several plants.
- Based on hint 3 (if there are k plants between two adjacent segments, there are k + 1 positions (ways) you could install the divider):
  - There will be `nbOfPlants + 1` ways to install a divider between two successive groups.
  - `nbOfPlants` is the number of plants between two successive groups (i.e., ignore the plants inside a single group).
- The answer is the number of ways to place a divider between each successive group times with each other.
- Define the answer as `long` to prevent potential overflows.

## Approach

- Initialise `nbOfSeats` and `nbOfPlants` to 0, and initialise `ans` to 1 (assume that there are at least two seats in the corridor).
- Range over `corridor` (say `corridor[i]` as `c`):
  - Increase `nbOfSeats` if `c` is a seat.
  - If `c` is a plant:
    - Increase `nbOfPlants` if we have already found a group (`nbOfSeats == 2`).
    - Otherwise, the plant is inside a single group, and we should ignore it.
  - After reaching the start of the next group (`nbOfSeats == 3`):
    - Update `ans`.
    - Set `nbOfSeats` to 1 (i.e., move to the next group of seats), and clear `nbOfPlants`.
- Return 0 if `nbOfSeats != 2` (i.e., there's an odd number of seats).
- Otherwise, return `ans`.

Pseudocode of `numberOfWays()`:

```
numberOfWays(corridor):
	Input corridor a string that contains only 'S's and 'P's
	Output number of ways to install dividers in this corridor
	
	nbOfSeats = 0
	nbOfPlants = 0
	ans = 1
	for every c in corridor:
		if c == 'S':
			nbOfSeats++
		else:
			if nbOfSeats == 2:
				nbOfPlants++
		end if
		if nbOfSeats == 3:
			ans = (ans * (nbOfPlants + 1)) % (1e9 + 7)
			nbOfSeats = 1
			nbOfPlants = 0
	end for
	if nbOfSeats != 2:
		return 0
	end if
	return ans
```

## Complexity
- Time complexity: $O(n)$.
  - $n$ iterations to calculate the answer.

- Space complexity: $O(1)$.

## Code
```c++
class Solution {
public:
  int MOD = 1e9 + 7;
  int numberOfWays(string corridor) {
    int nbOfSeats = 0;  // nbOfSeats is the number of seats in this group
    int nbOfPlants = 0;
    long ans = 1;

    for (char c : corridor) {
      if (c == 'S') {
        nbOfSeats++;
      } else {
        if (nbOfSeats == 2) {
          // Ignore plants inside a single group (i.e., only count plants between groups)
          nbOfPlants++;
        }
      }

      if (nbOfSeats == 3) {
        // This group reached its capacity
        ans = (ans * (nbOfPlants + 1)) % MOD;
        nbOfSeats = 1;  // Switch to the next group
        nbOfPlants = 0;
      }
    }

    // No answer if there're odd number of seats
    if (nbOfSeats != 2) {
      return 0;
    }
    return ans;
  }
};
```
