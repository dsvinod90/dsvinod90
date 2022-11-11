---
title: Permutation in String 
layout: default
filename: permutation_in_string 
--- 
[back](/dsvinod90/leetcode)

# [Permutation in String](https://leetcode.com/problems/permutation-in-string/submissions/840226479/)
###### tags: `Leetcode`, `Medium`, `Sliding Window`

## Python Code
``` python
"""
Approach: Sliding Window
Time Complexity: O(l1 + 26*(l2 - l1)), where l1, l2 = length of s1, length of s2
Space Complexity: O(1), because the map always stores exactly 26 elements
"""
import sys

class PermutationInString:
    # eg: s1='ab' s2='eidbaooo'
    def _check_inclusion(self, s1: str, s2: str) -> bool:
        # return false if size of s1 is smaller than size of s2
        if len(s1) > len(s2): return False
        # initialize two dictionaries corresponding to s1 and s2.
        # set every letter of the alphabet to have initial count as 0
        s1_count, s2_count = {}, {}
        for index in range(ord('a'), ord('z') + 1):
            s1_count.setdefault(chr(index), 0)
            s2_count.setdefault(chr(index), 0)
        # for the length of s1 set the count of every letter in s1_count and 
        # those many letters in s2_count
        for index in range(len(s1)):
            s1_letter, s2_letter = s1[index], s2[index]
            s1_count[s1_letter] += 1
            s2_count[s2_letter] += 1
        # initialize matches to keep track of match count
        # set matches to 0 initially
        # for every matching value of key in s1_count and s2_count,
        # increment matches
        matches = 0
        for index in range(ord('a'), ord('z') + 1):
            matches += 1 if s1_count[chr(index)] == s2_count[chr(index)] else 0
        # start from the next letter after len(s1) letters in the string s2
        left = 0
        for right in range(len(s1), len(s2)):
            # if match count is 26 then return true
            if matches == 26: return True
            # for every right index position, add 1 to its count dict
            letter = s2[right]
            s2_count[letter] += 1
            # if the count of that letter matches that of s1 then increment
            # matches else if the the count of that letter was matching with
            # s1_count and has now increased after incrementing in s2_count,
            # then decrement matches
            if s2_count[letter] == s1_count[letter]:
                matches += 1
            elif s1_count[letter] + 1 == s2_count[letter]:
                matches -= 1
            # move left pointer to the next index position and check for match
            # count in the same way as done above
            letter = s2[left]
            s2_count[letter] -= 1
            if s2_count[letter] == s1_count[letter]:
                matches += 1
            elif s1_count[letter] - 1 == s2_count[letter]:
                matches -= 1
            left += 1
        return matches == 26


    def process(self, str1: str, str2: str):
        print(f"\nOutput >> {self._check_inclusion(str1, str2)}\n")

if __name__ == "__main__":
    str1 = input("Enter s1: ")
    str2 = input("Enter str2: ")
    PermutationInString().process(str1, str2)
```

## Output
```shell
Enter s1: ab
Enter str2: eidbaooo

Output >> True


Process finished with exit code 0
```