---
title: Two Sum II - Input Array is Sorted 
layout: default
filename: two_sum_ii 
--- 
[back](/dsvinod90/leetcode)

# [Two Sum II - Input Array is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)
###### tags: `Leetcode`, `Medium`, `Two Pointers`

## Python Code
```python
"""
Approach: Two Pointer
Time Complexity: O(N)
Space Complexity: O(1)
"""

from typing import List


class TwoSumII:
    def _two_sum(self, numbers: List[int], target: int) -> List[int]:
        # Input list is already sorted
        # initialize left and right pointers at the beginning and end of the list
        left, right = 0, len(numbers) - 1
        # loop till left and right are at the same index value
        while left < right:
            # calculate sum
            result = numbers[left] + numbers[right]
            # if sum equals target value then return the 1-indexed positions of the pointers
            if result == target:
                return [left + 1, right + 1]
            # if sum is less than target then we need a bigger number for the result, hence move left pointer to the
            # next index position
            elif result < target:
                left += 1
            # if sum is greater than the target then we need a smaller number for the result, hence move the right
            # pointer to the previous index position
            else:
                right -= 1
        # return empty list if the target is not achievable by any of the values in the list
        return []

    def process(self, nums: List[int], t: int) -> None:
        print(f"\nOutput >> {self._two_sum(nums, t)}\n")


if __name__ == '__main__':
    size = int(input("Enter size of the list: "))
    print("Enter the values of the list: ")
    input_list = []
    for _ in range(size):
        input_list.append(int(input()))
    tar = int(input("Enter the target value: "))
    TwoSumII().process(input_list, tar)
```

## Output
```shell
Enter size of the list: 5
Enter the values of the list: 
10
12
23
58
63
Enter the target value: 73

Output >> [1, 5]


Process finished with exit code 0
```