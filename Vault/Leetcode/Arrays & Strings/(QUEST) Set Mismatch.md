
> [!question] PROBLEM STATEMENT
> You have a set of integers `s`, which originally contains all the numbers from `1` to `n`. Unfortunately, due to some error, one of the numbers in `s` got duplicated to another number in the set, which results in **repetition of one** number and **loss of another**number.
>
> You are given an integer array `nums` representing the data status of this set after the error.
> Find the number that occurs twice and the number that is missing and return _them in the form of an array_.
> 
> **Example 1:**> 
> **Input:** nums = [1,2,2,4]
> **Output:** [2,3]
> 
> **Example 2:**> 
> **Input:** nums = [1,1]
> **Output:** [1,2]> 


> [!info] THOUGHT PROCESS
> We must find the duplicate number and the missing number. Finding the duplicate number is easy, we can use a set to track duplicate membership.
> To find the missing number we must employ math.
> 
> To find the missing number, we can use the equation
> $$
> missing\ number = expected\ sum - actual\ sum + duplicate\ number
> $$
> Where
> $$
> expected\ sum = size\ of\ list * \dfrac{size\ of\ list + 1}2
> $$
> and *actual sum* is the sum of all numbers in the original list.

## Solution
```python
class Solution:
2    def findErrorNums(self, nums: List[int]) -> List[int]:
3        seen = set()
4        size = len(nums)
5        actual_sum = sum(nums)
6        expected_sum = int(size * (size + 1) / 2)    
7    
8        for number in nums:
9            if number in seen:
10                missing_num = expected_sum - actual_sum + number
11                return [number, missing_num]
12            seen.add(number)
```