---
title: Three Sum
layout: default
filename: three_sum 
--- 
[back](/dsvinod90/leetcode)

# [Three Sum](https://leetcode.com/problems/3sum/)
###### tags: `Leetcode`, `Medium`, `Two Pointers`

## Python Code
```python
"""
Approach: Two Pointer
Time Complexity: O(N^2)
Space Complexity: O(N)
"""

from typing import List


class ThreeSum:
    def _calculateThreeSum(self, nums: List[int]) -> List[List[int]]:
        # initialize result to be a list
        result = []
        # sort the input in ascending order so that we can use the two pointer approach with an outer loop
        nums.sort()
        # start outer loop
        for index in range(len(nums)):
            # no need to consider an element that has already occurred before as the results will not change
            if index > 0 and nums[index] == nums[index - 1]:
                continue
            # use the two pointer approach to check if the sum of all the three numbers sum to zero
            # start left on the next index position with respect to the outer index and right will be
            # pointing at the last element
            left, right = index + 1, len(nums) - 1
            while left < right:
                # calculate the sum of the three numbers being pointed by the indices
                temp_sum = nums[index] + nums[left] + nums[right]
                # if sum > 0 then decrement right pointer as we need to reduce the sum
                if temp_sum > 0:
                    right -= 1
                # if sum < 0 then increment the left pointer as we need to increase the sum
                elif temp_sum < 0:
                    left += 1
                else:
                    # if the sum is zero then add the three numbers to the result array and then increment the left
                    # pointer
                    result.append([nums[index], nums[left], nums[right]])
                    left += 1
                    # keep incrementing left pointer if the next number is the same as the previous number because
                    # it will produce duplicate triplets
                    while left < right and nums[left] == nums[left - 1]:
                        left += 1
        # return result list
        return result

    def process(self, nums: List[int]) -> None:
        print(f"\nOutput >> {self._calculateThreeSum(nums)}\n")


if __name__ == '__main__':
    no_of_elements = int(input("Enter the number of elements in the list: "))
    input_list = []
    print("Enter the values of the list: ")
    for _ in range(no_of_elements):
        input_list.append(int(input()))
    ThreeSum().process(input_list)
```

## Output
```shell
Enter the number of elements in the list: 6
Enter the values of the list: 
-1
0
1
2
-1
-4

Output >> [[-1, -1, 2], [-1, 0, 1]]


Process finished with exit code 0
```