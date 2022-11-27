---
title: Contains Duplicate
layout: default
filename: contains_duplicate 
--- 
[back](/dsvinod90/leetcode)

# [Contains Duplicates](https://leetcode.com/problems/contains-duplicate/)
###### tags: `Leetcode`, `Easy`, `Arrays and Hashing`

## Python Code
```python
"""
Approach: Arrays and Hashing
Time Complexity: O(N)
Space Complexity: O(N)
"""
from typing import List


class ContainsDuplicate:
    def _contains_duplicate(self, nums: List[int]) -> bool:
        # initialize a set. This will help us keep track of duplicates
        # The reason to consider a set is that it takes constant time to find an element in a set.
        visited = set()
        # iterate through the input list
        for num in nums:
            # if the number already exists in the visited set then it is a duplicate. Hence, return True.
            if num in visited:
                return True
            # if the number does not exist in the visited set then that's the first time it is encountered. Now, add it
            # to the visited set
            visited.add(num)
        # if the control reaches here, it means that there were no duplicates in the input list. Hence, return False
        return False

    def process(self, nums_list: List[int]) -> None:
        print(f"\nOutput >> {self._contains_duplicate(nums_list)}\n")


if __name__ == '__main__':
    no_of_elements = int(input("Enter the number of elements in the list: "))
    elements = []
    print("Enter the elements: ")
    for _ in range(no_of_elements):
        elements.append(int(input()))
    ContainsDuplicate().process(elements)
```

## Output
```shell
Enter the number of elements in the list: 4
Enter the elements: 
1
2
3
1

Output >> True
```