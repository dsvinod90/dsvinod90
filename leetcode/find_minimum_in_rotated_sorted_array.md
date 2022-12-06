---
title: Find Minimum In Rotated Sorted Array 
layout: default
filename: find_minimum_in_rotated_sorted_array 
--- 
[back](/dsvinod90/leetcode)

# [Find Minimum In Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)
###### tags: `Leetcode`, `Medium`, `Binary Search`

## Python Code
```python
"""
Approach: Binary Search
Time Complexity: O(log(N))
Space Complexity: O(1)
"""

from typing import List


class FindMinimumInRotatedSortedArray:
    def _find_min(self, nums: List[int]) -> int:
        """ Return the minimum number in the input list
        Fetches the minimum number in the input list that could be a rotated sorted array
        :param nums: list of integer values
        :return: integer in the list that is minimum
        """

        # declare and initialize left and right pointers to the first and last positions in the list
        left, right = 0, len(nums) - 1
        # if the left-most value is less than right-most value, it means that the array is already sorted
        if nums[left] <= nums[right]:
            # return the left-most value as it is the least
            return nums[left]
        # declare and initialize curr_min to hold the value as infinity
        curr_min = float("inf")
        # iterate through the input list
        while left <= right:
            # find the mid-index
            mid = (left + right) // 2
            # curr_min is the minimum value of curr_min and mid-value
            curr_min = min(curr_min, nums[mid])
            # if mid-value is greater than or equal to value at the right index, it means that mid-value is in the
            # left sorted array. We need to search to the right for the min value.
            if nums[mid] >= nums[right]:
                # move left pointer to the position after mid-index
                left = mid + 1
            # otherwise, mid-value is in the right sorted array. We need to search to the left for the min value.
            else:
                # move right pointer to the position before the mid-index
                right = mid - 1
        # return the curr_min value
        return int(curr_min)

    def process(self, input_nums: List[int]) -> None:
        print(f"\nOutput >> {self._find_min(input_nums)}\n")


if __name__ == '__main__':
    count = int(input("Enter the number of elements in the input list: "))
    input_nums_list = []
    print("Enter the numbers: ")
    for _ in range(count):
        input_nums_list.append(int(input()))
    FindMinimumInRotatedSortedArray().process(input_nums_list)
```

## Output
```shell
Enter the number of elements in the input list: 7
Enter the numbers: 
4
5
6
7
0
1
2

Output >> 0


Process finished with exit code 0
```