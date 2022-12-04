---
title: Top K Frequent Elements 
layout: default
filename: top_k_frequent_elements 
--- 
[back](/dsvinod90/leetcode)

# [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)
###### tags: `Leetcode`, `Medium`, `Arrays and Hashing`

## Python Code
```python
"""
Approach: Arrays and Hashing
Time Complexity: O(N)
Space Complexity: O(N)
"""

from typing import List


class TopKFrequentElements:
    def _top_k_frequent(self, nums: List[int], k: int) -> List[int]:
        # initialize frequency hash and result list
        frequency_hash, result = {}, []
        # initialize frequency list for every element in the input list
        frequency_list = [[] for _ in range(len(nums) + 1)]
        # for every number in the input list
        for number in nums:
            # keep count of the numbers in the input list by adding them to the frequency hash
            frequency_hash[number] = 1 + frequency_hash.get(number, 0)
        # key of the frequency hash is the number and the value is the frequency of that number in the list
        for number, count in frequency_hash.items():
            # the index position of frequency list represents the count.
            frequency_list[count].append(number)
        # iterate in reverse through the frequency list
        for index in range(len(frequency_list) - 1, -1, -1):
            # pick the k elements from the frequency list
            for number in frequency_list[index]:
                result.append(number)
                # if the result list had k elements, return the list
                if len(result) == k:
                    return result
        # if control reaches here then it could not find k elements and will return result
        return result

    def process(self, nums_list: List[int], k_val: int) -> None:
        print(f"\nOutput >> {self._top_k_frequent(nums_list, k_val)}\n")


if __name__ == '__main__':
    count = int(input("Enter the number of items in the input list: "))
    input_nums_list = []
    print("Enter the numbers: ")
    for _ in range(count):
        input_nums_list.append(int(input()))
    input_k_val = int(input("Enter the k value: "))
    TopKFrequentElements().process(input_nums_list, input_k_val)
```

## Output
```shell
Enter the number of items in the input list: 6
Enter the numbers: 
1
1
1
2
2
3
Enter the k value: 2

Output >> [1, 2]


Process finished with exit code 0
```