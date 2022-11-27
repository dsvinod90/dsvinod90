---
title: Container With Most Water
layout: default
filename: container_with_most_water 
--- 
[back](/dsvinod90/leetcode)

# [Container With Most Water](https://leetcode.com/problems/container-with-most-water/)
###### tags: `Leetcode`, `Medium`, `Two Pointers`

## Python Code
```python
"""
Approach: Two Pointer
Time Complexity: O(N)
Space Complexity: O(1)
"""

from typing import List


class ContainerWithMostWater:
    def _max_area(self, height: List[int]) -> int:
        # initialize left and right pointers to point at the first and last element of the input list
        left, right = 0, len(height) - 1
        # initialize result to be 0
        result = 0
        while left < right:
            # calculate the area between the two pointers
            area = min(height[left], height[right]) * (right - left)
            # result is the max area that is calculated until all iterations are complete
            result = max(result, area)
            # if the value at left is less than the one in right then increment the left pointer
            if height[left] < height[right]:
                left += 1
            # if the value at right is less than or equal to the one on the left then decrement right by one
            else:
                right -= 1
        # return the result
        return result

    def process(self, height_list: List[int]) -> None:
        print(f"\nOutput >> {self._max_area(height_list)}\n")


if __name__ == '__main__':
    no_of_elements = int(input("Enter number of elements in the list: "))
    elements = []
    print("Enter the elements: ")
    for _ in range(no_of_elements):
        elements.append(int(input()))
    ContainerWithMostWater().process(elements)
```

## Output
```shell
Enter number of elements in the list: 9
Enter the elements: 
1
8
6
2
5
4
8
3
7

Output >> 49


Process finished with exit code 0
```