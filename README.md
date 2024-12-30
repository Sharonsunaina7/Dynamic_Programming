# Dynamic_Programming
Counting ways to build good strings
# Counting Ways to Build Good Strings | Dynamic Programming Approach

## Problem Statement
Given the integers `zero`, `one`, `low`, and `high`, you can construct a string by starting with an empty string, and then at each step perform either of the following:

1. Append the character `'0'` `zero` times.
2. Append the character `'1'` `one` times.

This process can be repeated any number of times. A "good string" is defined as a string constructed using the above process that has a length between `low` and `high` (inclusive).

Return the number of different good strings that can be constructed satisfying these properties. Since the answer can be large, return it modulo $10^9 + 7$.

---

## Intuition

The problem revolves around efficiently counting strings of valid lengths without explicitly generating them. Here's the step-by-step breakdown:

### Key Observations:
1. **Length-Driven Problem**: The specific characters (`'0'` and `'1'`) in the string do not matter, only the length does. This allows us to frame the problem in terms of lengths rather than actual strings.

2. **Recursive Relationship**:
   - To form a string of length `i`, we can append `'0'` `zero` times to a string of length `i - zero`.
   - Similarly, we can append `'1'` `one` times to a string of length `i - one`.

3. **Dynamic Programming**: Using the above relation, we can compute the number of ways to form strings of increasing lengths up to `high`, storing intermediate results to avoid redundant calculations.

4. **Modulo Arithmetic**: Since the number of strings can grow very large, we use modulo $10^9 + 7$ at every step to ensure computations remain manageable.

---

## Approach

We use a **dynamic programming (DP)** array `dp` where `dp[i]` represents the number of ways to construct a string of length `i`.

### Steps:
1. Initialize `dp[0] = 1`, as there's one way to form an empty string.
2. Iterate over lengths from `1` to `high`:
   - If `i - zero >= 0`, add `dp[i - zero]` to `dp[i]`.
   - If `i - one >= 0`, add `dp[i - one]` to `dp[i]`.
3. Compute the total number of good strings by summing up `dp[i]` for all `i` in the range `[low, high]`.

---

## Complexity
- **Time Complexity**: $O(\text{high})$ – We iterate through all lengths up to `high`.
- **Space Complexity**: $O(\text{high})$ – We store the number of ways for each length in the `dp` array.

---

## Code Implementation
```python
class Solution:
    def countGoodStrings(self, low: int, high: int, zero: int, one: int) -> int:
        MOD = 10**9 + 7
        dp = [0] * (high + 1)
        dp[0] = 1  # Base case: One way to form an empty string

        for i in range(1, high + 1):
            if i - zero >= 0:
                dp[i] = (dp[i] + dp[i - zero]) % MOD
            if i - one >= 0:
                dp[i] = (dp[i] + dp[i - one]) % MOD

        # Sum up the ways to form strings of length between low and high
        return sum(dp[low:high + 1]) % MOD
```

---

## Example

### Input:
```python
low = 3
high = 3
zero = 1
one = 1
```

### Output:
```python
8
```

### Explanation:
All good strings of length 3 are:
- Using `'0'` once and `'1'` twice: "001", "010", "100"
- Using `'1'` once and `'0'` twice: "110", "101", "011"
- Using `'0'` three times: "000"
- Using `'1'` three times: "111"

Sure! Here's a write-up for your GitHub post explaining the problem and its solution:

---

### Example Walkthrough

#### Input:
`low = 3, high = 5, zero = 2, one = 2`

#### Steps:
1. **Initialize `dp`**:  
   `dp = [1, 0, 0, 0, 0, 0]`

2. **Iterate through lengths**:
   - \(i = 2\):  
     Append `'0'` (length 2) → `dp[2] = dp[2 - 2] = 1`  
     Append `'1'` (length 2) → `dp[2] = dp[2 - 2] + 0 = 1`
   - \(i = 3\):  
     No updates since \(i < \text{zero}\) and \(i < \text{one}\).  
   - \(i = 4\):  
     Append `'0'` (length 2) → `dp[4] = dp[4 - 2] = 1`  
     Append `'1'` (length 2) → `dp[4] += dp[4 - 2] = 2`
   - \(i = 5\):  
     Append `'0'` (length 2) → `dp[5] = dp[5 - 2] = 2`  
     Append `'1'` (length 2) → `dp[5] += dp[5 - 2] = 2`

3. **Sum `dp` for lengths 3 to 5**:
   \( dp[3] + dp[4] + dp[5] = 0 + 2 + 2 = 4 \)

#### Output:
`4`

---

## Tags
- Dynamic Programming
- Modular Arithmetic
- Problem Solving

