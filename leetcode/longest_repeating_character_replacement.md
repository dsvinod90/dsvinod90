---
title: Longest Repeating Character Replacement 
layout: default
filename: longest_repeating_character_replacement 
--- 
[back](/dsvinod90/leetcode)

# [Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/)
###### tags: `Leetcode`, `Medium`, `Sliding Window`

## Python Code
```python
"""
Approach: Sliding Window
Time Complexity: O(N)
Space Complexity: O(N)
"""


class LongestRepeatingCharacterReplacement:
    def _character_replacement(self, s: str, k: int) -> int:
        result = 0
        # initialize count map to keep track of the count of the letters in the current window
        count = {}
        # set left pointer to be at 0th index
        left = 0
        # iterate right pointer from 0 till the length of the string
        for right in range(len(s)):
            # increment count of that letter in the hashmap
            count[s[right]] = 1 + count.get(s[right], 0)
            # if window_length - max occurrence of characters in hashmap is more  than k, then move left pointer to
            # the next index
            while (right - left + 1) - max(count.values()) > k:
                # since left pointer has moved count of the letter it was previously pointing at should be decremented
                count[s[left]] -= 1
                left += 1
            # result is the maximum window_length
            result = max(result, (right - left + 1))
        return result

    def process(self, string: str, k: int) -> None:
        print(f"\nOutput >> {self._character_replacement(string, k)}\n")


if __name__ == "__main__":
    input_string = input("Enter the string: ")
    replacements = int(input("Enter the number of replacements: "))
    LongestRepeatingCharacterReplacement().process(input_string, replacements)

```

## Output
```shell!
Enter the string: ABBABAB
Enter the number of replacements: 1

Output >> 4


Process finished with exit code 0
```