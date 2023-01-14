---
title: Find Duplicate Number 
layout: default
filename: 
--- 
[back](/dsvinod90/leetcode)

# [Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/)
###### tags: `Leetcode`, `Medium`, `Linked List`

## Python Code
```python
"""
Approach: Linked List
Time Complexity: O(N)
Space Complexity: O(1)
"""

from typing import List


class FindDuplicateNumber:
    def _find_duplicate(self, nums: List[int]) -> int:
        """ Return the first index of the repeating number
        Accept a list input and return the repeating number in the list
        :param nums: List input of numbers
        :return: Integer representing the repeating number in the list
        """

        # declare and initialize a slow and fast pointer starting at the first position of the list
        slow, fast = 0, 0
        # loop until slow and fast point are pointing at duplicates
        while True:
            # we consider the index as the node and the value as the index that node points to.
            # slow moves one node and fast moves two nodes
            slow = nums[slow]
            fast = nums[nums[fast]]
            # if slow is equal to fast then we have found the cycle, and we break the loop
            if slow == fast:
                break
        # start another pointer at 0 index
        slow2 = 0
        # iterate until slow equals slow2. This will be the node that marks the start of the cycle
        while True:
            # shift slow and slow2 by one node
            slow = nums[slow]
            slow2 = nums[slow2]
            # if slow equals slow2 return slow. That will be the node that marks the start of the cycle
            if slow == slow2:
                return slow

    def process(self, input_nums: List[int]) -> None:
        print(f"\nOutput >> {self._find_duplicate(input_nums)}\n")


if __name__ == '__main__':
    input_nums_size = int(input("Enter the size of the list: "))
    input_nums_list = []
    print("Enter the numbers in the list:")
    for index in range(input_nums_size):
        input_nums_list.append(int(input(f"\tEnter the value at index {index}: ")))
    FindDuplicateNumber().process(input_nums_list)
```

## Output
```shell
Enter the size of the list: 5
Enter the numbers in the list:
	Enter the value at index 0: 3
	Enter the value at index 1: 1
	Enter the value at index 2: 3
	Enter the value at index 3: 4
	Enter the value at index 4: 2

Output >> 3


Process finished with exit code 0
```