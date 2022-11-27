---
title: Valid Anagram
layout: default
filename: valid_anagram 
--- 
[back](/dsvinod90/leetcode)

# [Valid Anagram](https://leetcode.com/problems/valid-anagram/)
###### tags: `Leetcode`, `Easy`, `Arrays and Hashing`

## Python Code
```python
"""
Approach: Arrays and Hashing
Time Complexity: O(N)
Space Complexity: O(1)
"""

class ValidAnagram:
    def _is_anagram(self, s: str, t: str) -> bool:
        # if the two strings of different lengths they cannot be anagrams. Hence, return False.
        if len(s) != len(t):
            return False
        # initialize a string map that will keep count of the letters appearing in the inputs
        s_map, t_map = {}, {}
        # get the count of every character in strings s and t. Strings s and t will have same length at this point.
        for index in range(len(s)):
            s_map[s[index]] = 1 + s_map.get(s[index], 0)
            t_map[t[index]] = 1 + t_map.get(t[index], 0)
        # iterate through every character of string s and check if the count of that character in s_map and t_map. If
        # they are unequal, return False.
        for character in s:
            if s_map.get(character, 0) != t_map.get(character, 0):
                return False
        # if the control reaches this point, it means that all the characters in s_map have equated to t_map. Hence,
        # s and t are anagram.
        return True

    def process(self, s_string: str, t_string: str) -> None:
        print(f"\n Output >> {self._is_anagram(s_string, t_string)}\n")


if __name__ == '__main__':
    string1 = input("Enter first string: ")
    string2 = input("Enter second string: ")
    ValidAnagram().process(string1, string2)
```

## Output
```shell
Enter first string: anagram
Enter second string: nagaram

 Output >> True


Process finished with exit code 0
```