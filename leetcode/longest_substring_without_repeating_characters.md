---
title: Longest Substring Without Repeating Characters 
layout: default
filename: longest_substring_without_repeating_characters 
--- 
[back](/dsvinod90/leetcode)

# [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
###### tags: `Leetcode`, `Medium`, `Sliding Window`

## Python Code
```python
"""
Approach: Sliding Window
Time Complexity: O(N)
Space Complexity: O(N)
"""


class LongestSubstringWithoutRepeatingCharacters:
    def _length_of_longest_substring(self, s: str) -> int:
        result = 0
        # count of the removed letters from the substring
        removed = 0
        # set to keep track of letters that do not repeat as we iterate through the string input
        visited = set()
        # iterate through every character of the input string
        for index in range(len(s)):
            # check if the character is present in the visited set. Keep removing characters from the left of the input
            # string until the current character is not present in the visited set.
            while s[index] in visited:
                # remove characters from the set starting from 0th index of the string
                visited.remove(s[removed])
                # increment removed count everytime a character is removed
                removed += 1
            # add the current character to the visited set
            visited.add(s[index])
            # result is the max value of all the lengths of the valid substrings
            result = max(result, index - removed + 1)
        return result

    def process(self, input_string: str):
        print(f"\nOutput >> {self._length_of_longest_substring(input_string)}\n")


if __name__ == '__main__':
    string = input("Enter input string: ")
    LongestSubstringWithoutRepeatingCharacters().process(string)
```

## Output
```shell!
Enter input string: anbkrancbc

Output >> 6


Process finished with exit code 0
```
