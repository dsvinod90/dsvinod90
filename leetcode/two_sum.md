---
title: Two Sum 
layout: default
filename: two_sum 
--- 
[back](/dsvinod90/leetcode)

# [Two Sum](https://leetcode.com/problems/two-sum/)
###### tags: `Leetcode`, `Easy`, `Arrays and Hashing`

## Python Code
```python
"""
Approach: Arrays and Hashing
Time Complexity: O(N)
Space Complexity: O(N)
"""

from typing import List


class TwoSum:
    def _two_sum(self, nums: List[int], target: int) -> List[int]:
        # initialize a hash that will keep track of the number and its index value in the input list
        nums_hash = {}
        # iterate through the numbers in the input list
        for index, number in enumerate(nums):
            # if target - number exists in the hash then we have found the two numbers that will add up to that target
            if (target - number) in nums_hash:
                # return the index value of the current number and its difference from target
                return [index, nums_hash[target - number]]
            # if target - number does not exist in the hash then we have not found the two numbers.
            # assign the index value to the number in the hash
            nums_hash[number] = index
        # if the control reaches here, then there are no values in the input list that can add up to the target.
        # return an empty list
        return []

    def process(self, nums_list: List[int], target_value: int) -> None:
        print(f"\nOutput >> {self._two_sum(nums_list, target_value)}\n")


if __name__ == '__main__':
    input_nums_list = []
    count = int(input("Enter the size of the list: "))
    print("Enter the values for the list: ")
    for _ in range(count):
        input_nums_list.append(int(input()))
    target_val = int(input("Enter the target value: "))
    TwoSum().process(input_nums_list, target_val)
```

## Output
```shell
Enter the size of the list: 4
Enter the values for the list: 
2
7
11
15
Enter the target value: 9

Output >> [1, 0]


Process finished with exit code 0
```