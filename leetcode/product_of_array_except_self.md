---
title: Product of Array Except Self 
layout: default
filename: product_of_array_except_self 
--- 
[back](/dsvinod90/leetcode)

# [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)
###### tags: `Leetcode`, `Medium`, `Arrays and Hashing`

## Python Code
```python
"""
Approach: Arrays and Hashing
Time Complexity: O(N)
Space Complexity: O(1)
"""

from typing import List


class ProductOfArrayExceptSelf:
    def _product_except_self(self, nums: List[int]) -> List[int]:
        # initialize pre and post values to 1
        pre, post = 1, 1
        # initialize result array to be of the same length as nums and set initial value as 1
        result = [1] * len(nums)
        # iterate through every number in the input list
        # pre-block
        for index, num in enumerate(nums):
            # the value at that index position in result = pre
            result[index] = pre
            # pre = pre * value of number at that index in nums list
            pre = pre * num
        # iterate through every item in the result list
        # post-block
        for index in range(len(result) - 1, -1, -1):
            # value of result at that index = post * value of result at that index calculate by pre-block
            result[index] = post * result[index]
            # post = post * value of number at the same index in nums list
            post = post * nums[index]
        # return result list
        return result

    def process(self, nums_list: List[int]) -> None:
        print(f"\nOutput >> {self._product_except_self(nums_list)}\n")


if __name__ == '__main__':
    count = int(input("Enter the number of elements in the list: "))
    input_nums_list = []
    print("Enter the numbers: ")
    for _ in range(count):
        input_nums_list.append(int(input()))
    ProductOfArrayExceptSelf().process(input_nums_list)
```

## Output
```shell
Enter the number of elements in the list: 4
Enter the numbers: 
1
2
3
4

Output >> [24, 12, 8, 6]


Process finished with exit code 0
```