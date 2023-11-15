---
title: HackerRank Extra Long Factorials
lang: en
date: 2023-11-15 21:12:24
tags:
    - HackerRank
    - Algorithm
    - Large numbers
categories:
    - HackerRank
---

## Link to this problem

[HackerRank Extra Long Factorials](https://www.hackerrank.com/challenges/extra-long-factorials/problem)

## Intuition

- Implement large number multiplication using a string or an array.

## Approach

1. Create an array called `largeInteger`, which represents a large number.
2. Fill the `largeInteger`  with `n`.
3. Iterate over numbers from `n` to 0:
   1. Multiply `largeInteger` by this number.
   2. Handle the potential carry.
4. Output the content of `largeInteger` to stdout.

Pseudocode of `largeIntMultiply`:

```
largeIntMultiply(largeInt, n):
	Input largeInt a very large number represent by an array
		n the multiplier
	Output the largeInt multiplied by n
	carry = 0
	for every i from largeInt.size()-1 to 0:
		number = n * largeInt[i] + carry
		largeInt[i] = number % 10
		carry = number / 10
		if i == 0 and carry != 0:
			add a 0 at the beginning of largeInt
			i++
		end if
	end for
	return largeInt
```

Pseudocode of `extraLongFactorials`:

```
extraLongFactorials(n):
	Input n the number to be calculated
	
	largeInteger = empty array
	i = n
	for i != 0:
		add i % 10 to the beginning of largeInteger 
		i /= 10
	end for
	for every i from n-1 to 2:
		largeInteger = largeIntMultiply(largeInteger, i)
	end for
	output largeInteger to stdout
```

## Complexity

Time complexity: $O(n^2)$.

- $n$ iterations to calculate the factorial.
- In each iteration:
  - Multiply the vector with the number is $O(n)$.
- Overall complexity is $O(n^2)$. 

Space complexity: $O(n)$.

## Code

```c++
void largeIntMultiply(vector<int> &largeInt, int n);
void extraLongFactorials(int n) {
    // Convert int to vercor<int>
    vector<int> largeInteger;
    for (int i = n; i != 0; i /= 10) {
        largeInteger.insert(largeInteger.begin(), i % 10);
    }
    for (int i = n-1; i >= 2; i--) {
        largeIntMultiply(largeInteger, i);
    }
    for (int i : largeInteger) {
        cout << i;
    }
}

void largeIntMultiply(vector<int> &largeInt, int n) {
    int carry = 0;
    for (int i = largeInt.size()-1; i >= 0; i--) {
        int number = largeInt[i] * n + carry;
        largeInt[i] = number % 10;
        carry = number / 10;
        if (i == 0 && carry != 0) {
            largeInt.insert(largeInt.begin(), 0);
            i++;
        }
    }
}
```
