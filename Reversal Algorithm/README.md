# 189. Rotate Array

[![LeetCode](https://img.shields.io/badge/LeetCode-189-orange)](https://leetcode.com/problems/rotate-array/)
[![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)](https://leetcode.com/problems/rotate-array/)
[![Language](https://img.shields.io/badge/Language-Python-blue)](https://www.python.org/)

## Problem Statement

Given an integer array `nums`, rotate the array to the right by `k` steps, where `k` is a non-negative integer.

The rotation must be performed **in-place**, meaning you should modify the original array without creating another array.

### Example 1

**Input:**
```python
nums = [1, 2, 3, 4, 5, 6, 7]
k = 3
```

**Output:**
```python
[5, 6, 7, 1, 2, 3, 4]
```

**Explanation:**

Rotate the array to the right by 3 positions:
- Move 7 to the first position.
- Move 6 to the second position.
- Move 5 to the third position.
- Shift the remaining elements to the right.

### Example 2

**Input:**
```python
nums = [-1, -100, 3, 99]
k = 2
```

**Output:**
```python
[3, 99, -1, -100]
```

## Approach: Reversal Algorithm

The Reversal Algorithm rotates an array using three reversal operations.

Instead of shifting elements individually, we reverse specific portions of the array to achieve the required rotation efficiently.

### Step 1: Handle Large Rotation Values Using Modulo

```python
k %= len(nums)
```

**Why do we use modulo?**

If the array contains 5 elements, rotating it 5 times brings it back to its original arrangement.

Therefore:
- 5 rotations = 0 effective rotations
- 7 rotations = 2 effective rotations
- 10 rotations = 0 effective rotations
- 12 rotations = 2 effective rotations

Modulo reduces unnecessary rotations.

### Step 2: Reverse the Entire Array

Reverse all elements in the array.

**Before:**
```python
[1, 2, 3, 4, 5, 6, 7]
```

**After:**
```python
[7, 6, 5, 4, 3, 2, 1]
```

### Step 3: Reverse the First K Elements

Reverse the first `k` elements.

Here, `k = 3`.

**Before:**
```python
[7, 6, 5, 4, 3, 2, 1]
```

**After:**
```python
[5, 6, 7, 4, 3, 2, 1]
```

### Step 4: Reverse the Remaining Elements

Reverse the remaining elements starting from index `k`.

**Before:**
```python
[5, 6, 7, 4, 3, 2, 1]
```

**After:**
```python
[5, 6, 7, 1, 2, 3, 4]
```

The required rotation is now complete!

## Python Solution

```python
class Solution:

    def reverse(self, nums, start, end):
        while start < end:
            nums[start], nums[end] = nums[end], nums[start]

            start += 1
            end -= 1

    def rotate(self, nums: list[int], k: int) -> None:
        """
        Rotate the array to the right by k positions.
        Modify the original array in-place.
        """

        if not nums:
            return

        # Handle rotations greater than array length
        k %= len(nums)

        # Step 1: Reverse the entire array
        self.reverse(nums, 0, len(nums) - 1)

        # Step 2: Reverse the first k elements
        self.reverse(nums, 0, k - 1)

        # Step 3: Reverse the remaining elements
        self.reverse(nums, k, len(nums) - 1)
```

## Understanding the Reverse Function

The reverse function uses two pointers:
- `start`: Points to the beginning of the selected portion.
- `end`: Points to the end of the selected portion.

It swaps both elements and moves the pointers towards the center until they meet.

```python
def reverse(self, nums, start, end):

    while start < end:

        nums[start], nums[end] = nums[end], nums[start]

        start += 1
        end -= 1
```

This performs the reversal in-place without creating another array.

## Complete Dry Run

**Input:**
```python
nums = [1, 2, 3, 4, 5, 6, 7]
k = 3
```

| Operation | Array |
|---|---|
| Original array | `[1, 2, 3, 4, 5, 6, 7]` |
| Reverse entire array | `[7, 6, 5, 4, 3, 2, 1]` |
| Reverse first 3 elements | `[5, 6, 7, 4, 3, 2, 1]` |
| Reverse remaining elements | `[5, 6, 7, 1, 2, 3, 4]` |

**Final Output:**
```python
[5, 6, 7, 1, 2, 3, 4]
```

## Edge Cases

| Input | Expected Output | Explanation |
|---|---|---|
| `nums = [1], k = 3` | `[1]` | Single element |
| `nums = [1, 2], k = 1` | `[2, 1]` | Rotate once |
| `nums = [1, 2, 3], k = 0` | `[1, 2, 3]` | No rotation |
| `nums = [1, 2, 3], k = 3` | `[1, 2, 3]` | Full rotation |
| `nums = [1, 2, 3], k = 5` | `[2, 3, 1]` | Modulo reduces k to 2 |

## Complexity Analysis

### Time Complexity: O(n)

We perform three reversal operations:
1. Reverse the entire array: O(n)
2. Reverse the first k elements: O(k)
3. Reverse the remaining n-k elements: O(n-k)

Total:

`O(n) + O(k) + O(n-k) = O(3n) = O(n)`

### Auxiliary Space Complexity: O(1)

- No additional array is created.
- Elements are swapped directly in the original array.
- Only two pointers (`start` and `end`) are used.

Therefore, the algorithm uses constant auxiliary space.

## Key Takeaways

1. Modulo (`%`) helps reduce unnecessary rotations.
2. Two-pointer technique is used to reverse an array.
3. Three reversal operations achieve right rotation.
4. The original array is modified in-place.
5. The algorithm achieves O(n) time and O(1) auxiliary space.

## Concepts Practiced

- Arrays
- Two Pointers
- In-place Array Manipulation
- Modulo Operator
- Reversal Algorithm
- Time and Space Complexity Analysis

## LeetCode Reference

[189. Rotate Array – LeetCode](https://leetcode.com/problems/rotate-array/)

**Approach:** Reversal Algorithm  
**Language:** Python  
**Difficulty:** Medium  
**Time Complexity:** O(n)  
**Space Complexity:** O(1)