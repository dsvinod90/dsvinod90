---
title: Group Anagrams 
layout: default
filename: group_anagrams 
--- 
[back](/dsvinod90/leetcode)

# [Group Anagrams](https://leetcode.com/problems/group-anagrams/)
###### tags: `Leetcode`, `Medium`, `Arrays and Hashing`

## Python Code
```python
"""
Approach: Arrays and Hashing
Time Complexity: O(N.K)
Space Complexity: O(N.K)
"""

from collections import defaultdict
from typing import List


class GroupAnagrams:
    def _group_anagrams(self, strs: List[str]) -> List[List[str]]:
        # initialize a result hash to have values as list
        result_hash = defaultdict(list)
        # iterate through every word in the input list
        for word in strs:
            # for every work initialize a freq list to hold 26 values (one for each letter of the alphabet) with initial
            # value as 0
            freq = [0] * 26
            # iterate through every character of the word
            for char in word:
                # increment corresponding index value of that character by one
                freq[ord(char) - ord('a')] += 1
            # convert the frequency list to a tuple and append the word to the list in the hash
            result_hash[tuple(freq)].append(word)
        # return all the values of the result_hash
        return result_hash.values()

    def process(self, input_list: List[str]) -> None:
        print(f"\nOutput >> {self._group_anagrams(input_list)}\n")


if __name__ == '__main__':
    input_string_list = []
    count = int(input("Enter the number of words in the input list: "))
    print("Enter the words: ")
    for _ in range(count):
        input_string_list.append(input())
    GroupAnagrams().process(input_string_list)
```

## Output
```shell
/usr/bin/python3 /Users/vinoddalavai/Dev/group_anagrams.py 
Enter the number of words in the input list: 6
Enter the words: 
eat
tea
tan
ate
nat
bat

Output >> dict_values([['eat', 'tea', 'ate'], ['tan', 'nat'], ['bat']])


Process finished with exit code 0
```