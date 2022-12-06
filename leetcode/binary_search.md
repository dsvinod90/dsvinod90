---
title: Binary Search
layout: default
filename: binary_search 
--- 
[back](/dsvinod90/leetcode)

# [Binary Search](https://leetcode.com/problems/binary-search/)
###### tags: `Leetcode`, `Medium`, `Binary Search`

## Python Code
```python
"""
Approach: Binary Search
Time Complexity: O(log(N))
Space Complexity: O(1)
"""

from typing import List


class BinarySearch:
    def _search(self, nums: List[int], target: int) -> int:
        """ Return index of the target element
        Search for the target value using binary search technique
        :param nums: list of integers
        :param target: value to be found in the list
        :return: integer value representing the index of the target value in the list. If not found, return -1
        """

        # declare and initialize left and right pointers to point at the 0th and last index of the input list
        left, right = 0, len(nums) - 1
        # loop until left and right pointers cross each other
        while left <= right:
            # calculate the mid-index between left and right
            mid = (right + left) // 2
            # return the mid-index if the number at this index is equal to target
            if nums[mid] == target:
                return mid
            # if number at mid-index is less than target then search needs to be narrowed to right of mid.
            if nums[mid] < target:
                # new left pointer will point to the next index value of mid
                left = mid + 1
            # if number at mid-index is more than target then search needs to be narrowed to the left of mid
            else:
                # new right pointer will point to the previous index value of mid
                right = mid - 1
        # if control reaches here then the target value was not found in the input list. Hence, return -1
        return -1

    def process(self, input_nums: List[int], input_target: int) -> None:
        print(f"\nOutput >> {self._search(input_nums, input_target)}\n")


if __name__ == '__main__':
    count = int(input("Enter the number of elements in the input list: "))
    input_nums_list = []
    print("Enter the numbers: ")
    for _ in range(count):
        input_nums_list.append(int(input()))
    input_target_value = int(input("Enter the target value: "))
    BinarySearch().process(input_nums_list, input_target_value)
```

## Output
```shell
Enter the number of elements in the input list: 6
Enter the numbers: 
-1
0
3
5
9
12
Enter the target value: 9

Output >> 4


Process finished with exit code 0
```