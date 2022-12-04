---
title: Longest Consecutive Sequence
layout: default
filename: longest_consecutive_sequence 
--- 
[back](/dsvinod90/leetcode)

# [Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/)
###### tags: `Leetcode`, `Medium`, `Arrays and Hashing`

## Python Code
```python
"""
Approach: Arrays and Hashing
Time Complexity: O(N)
Space Complexity: O(N)
"""

from typing import List


class LongestConsecutiveSequence:
    def _longest_consecutive(self, nums: List[int]) -> int:
        # initialize result to 0
        result = 0
        # initialize a set which will have values of nums
        nums_set = set(nums)
        # iterate through the numbers in input list
        for num in nums:
            # check if number - 1 does not exist in the set. This means that the current number is the lowest in
            # its sequence
            if num - 1 not in nums_set:
                # set count to 1
                count = 1
                # loop until number + count is present in the set
                while num + count in nums_set:
                    # keep incrementing count
                    count += 1
                # result is the max value of count calculated for the input list
                result = max(count, result)
        # return result
        return result

    def process(self, input_nums: List[int]) -> None:
        print(f"\nOutput >> {self._longest_consecutive(input_nums)}\n")


if __name__ == '__main__':
    no_of_elements = int(input("Enter the number of elements in the list: "))
    input_nums_list = []
    print("Enter the numbers into the list: ")
    for _ in range(no_of_elements):
        input_nums_list.append(int(input()))
    LongestConsecutiveSequence().process(input_nums_list)
```

## Output
```shell
Enter the number of elements in the list: 6
Enter the numbers into the list: 
100
4
200
1
3
2

Output >> 4


Process finished with exit code 0
```