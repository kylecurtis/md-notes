Topics: `Array`, `Hash Table`

Link: https://leetcode.com/problems/two-sum/description/

<br>

---

<br>

## Description

<br>

Given an array of integers `nums` and an integer `target`, return _indices of the two numbers such that they add up to `target`_.

You may assume that each input would have **_exactly_ one solution**, and you may not use the _same_ element twice.

You can return the answer in any order.

<br>

---

<br>


## Examples

<br>

**Example 1:**

**Input:** nums = [2,7,11,15], target = 9

**Output:** [0,1]

**Explanation:** Because nums[0] + nums[1] == 9, we return [0, 1].

<br>

**Example 2:**

**Input:** nums = [3,2,4], target = 6

**Output:** [1,2]

<br>

**Example 3:**

**Input:** nums = [3,3], target = 6

**Output:** [0,1]

<br>

---

<br>

## Constraints 

<br>

$2$ <= nums.length <= $10^4$

$-10^9$ <= nums[i] <= $10^9$

$-10^9$ <= target <= $10^9$

**Only one valid answer exists.**

<br>

**Follow-up:** Can you come up with an algorithm that is less than $O(n^2)$ time complexity?

<br>

---

<br>

## Hints

<br>

1. A really brute force way would be to search for all possible pairs of numbers but that would be too slow. Again, it's best to try out brute force solutions for just for completeness. It is from these brute force solutions that you can come up with optimizations.

<br>

2. So, if we fix one of the numbers, say `x`, we have to scan the entire array to find the next number `y` which is `value - x` where value is the input parameter. Can we change our array somehow so that this search becomes faster?

<br>

3. The second train of thought is, without changing the array, can we use additional space somehow? Like maybe a hash map to speed up the search?

<br>

---

<br>


## Approach 1: Brute Force

The brute force approach is simple. Loop through each element `x` and find if there is another value that equals to `target − x`.

<br>

#### Implementation

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums)):
            for j in range(i + 1, len(nums)):
                if nums[j] == target - nums[i]:
                    return [i, j]
```

<br>

---

<br>

#### Complexity Analysis

<br>

Time complexity: $O(n^2)$.  

For each element, we try to find its complement by looping through the rest of the array which takes $O(n)$ time. Therefore, the time complexity is $O(n^2)$.

<br>

Space complexity: $O(1)$.  

The space required does not depend on the size of the input array, so only constant space is used.

<br>

---

<br>

## Approach 2: Two-pass Hash Table

<br>

#### Intuition

To improve our runtime complexity, we need a more efficient way to check if the complement exists in the array. If the complement exists, we need to get its index. What is the best way to maintain a mapping of each element in the array to its index? **A hash table**.

We can reduce the lookup time from $O(n)$ to $O(1)$ by trading space for speed. A hash table is well suited for this purpose because it supports fast lookup in _near_ constant time. I say "near" because if a collision occurred, a lookup could degenerate to $O(n)$ time. However, lookup in a hash table should be amortized $O(1)$ time as long as the hash function was chosen carefully.

<br>

#### Algorithm

A simple implementation uses two iterations. In the first iteration, we add each element's value as a key and its index as a value to the hash table. Then, in the second iteration, we check if each element's complement (`target − nums[i]`) exists in the hash table. If it does exist, we return current element's index and its complement's index. Beware that the complement must not be `nums[i]` itself!

<br>

---

<br>

#### Implementation

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hashmap = {}
        for i in range(len(nums)):
            hashmap[nums[i]] = i
        for i in range(len(nums)):
            complement = target - nums[i]
            if complement in hashmap and hashmap[complement] != i:
                return [i, hashmap[complement]] 
```

<br>

---

<br>

#### Complexity Analysis

<br>

Time complexity: $O(n)$.  

We traverse the list containing nnn elements exactly twice. Since the hash table reduces the lookup time to $O(1)$, the overall time complexity is $O(n)$.

<br>

Space complexity: $O(n)$.  
    
The extra space required depends on the number of items stored in the hash table, which stores exactly nnn elements.

