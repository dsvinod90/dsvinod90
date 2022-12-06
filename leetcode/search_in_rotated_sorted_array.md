---
title: Search In Rotated Sorted Array 
layout: default
filename: search_in_rotated_sorted_array 
--- 
[back](/dsvinod90/leetcode)

# [Search In Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)
###### tags: `Leetcode`, `Medium`, `Binary Search`

## Python Code
```python
"""
Approach: Binary Search
Time Complexity: O(log(N))
Space Complexity: O(1)
"""

from typing import List


class SearchInRotatedSortedArray:
    def _search(self, nums: List[int], target: int) -> int:
        """ Return the index position of the target in the input list
        Search for the target value in the rotated sorted list of numbers and return the index at which it occurs
        :param nums: list of numbers
        :param target: value to be searched for in the input list
        :return: integer value representing the index position in the nums list where the target appears.
        Returns -1 if not found
        """

        # declare and initialize left and right pointers to the first and last position of the input list
        left, right = 0, len(nums) - 1
        # loop through the nums list
        while left <= right:
            # find the mid-element
            mid = (left + right) // 2
            # if number at mid-index is equal to the target then return the mid-index
            if nums[mid] == target:
                return mid
            # if number at mid-index is greater than or equal to the numbers on the left index then it means that
            # the mid-index belongs to the left sorted array
            if nums[mid] >= nums[left]:
                # if target is greater than or equal to number at left-index and less than or equal to
                # number at mid-index
                if nums[mid] >= target >= nums[left]:
                    # narrow search to the left
                    right = mid - 1
                # otherwise narrow search to the right
                else:
                    left = mid + 1
            # otherwise number at mid-index belongs to the right sorted array
            else:
                # if target is less than number at mid-index or greater than number at right index
                if target < nums[mid] or target > nums[right]:
                    # narrow search to the left
                    right = mid - 1
                # otherwise narrow search to the right
                else:
                    left = mid + 1
        # if control reaches here it means that the target is not found in the input list. Hence, return -1
        return -1

    def proceed(self, input_nums: List[int], input_target: int) -> None:
        print(f"\nOutput >> {self._search(input_nums, input_target)}\n")


if __name__ == '__main__':
    count = int(input("Enter the number of integers in the input list: "))
    input_nums_list = []
    print("Enter the numbers: ")
    for _ in range(count):
        input_nums_list.append(int(input()))
    input_target_value = int(input("Enter the target value to be searched for: "))
    SearchInRotatedSortedArray().proceed(input_nums_list, input_target_value)
```

## Output
```shell
Enter the number of integers in the input list: 7
Enter the numbers: 
4
5
6
7
0
1
2
Enter the target value to be searched for: 0

Output >> 4


Process finished with exit code 0
```