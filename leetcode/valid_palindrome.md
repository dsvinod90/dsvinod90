---
title: Valid Palindrome 
layout: default
filename: valid_palindrome 
--- 
[back](/dsvinod90/leetcode)

# [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)
###### tags: `Leetcode`, `Easy`, `Two Pointers`

## Python Code
```python
"""
Approach: Two Pointer
Time Complexity: O(N)
Space Complexity: O(1)
"""


class ValidPalindrome:
    def _is_palindrome(self, s: str) -> bool:
        # initialize left and right pointer to the beginning and end of the string respectively
        left, right = 0, len(s) - 1
        # iterate until left and right are at the same index
        while left <= right:
            # skip characters that are not letters or numbers
            if not s[left].isalnum():
                left += 1
            elif not s[right].isalnum():
                right -= 1
            # check for same letter at both pointers (case-insensitive)
            elif s[left].lower() == s[right].lower():
                # move left and right pointers one position towards each other if left and right letters are the same
                left += 1
                right -= 1
            else:
                # if the letters are different at both the pointers then return False
                return False
        # control will reach here if all the letters at both pointers have matched. Hence, return true
        return True

    def process(self, input_string: str) -> None:
        print(f"\nOutput >> {self._is_palindrome(input_string)}\n")


if __name__ == '__main__':
    string = input("Enter string to check for palindrome: ")
    ValidPalindrome().process(string)
```

## Output
```shell
Enter string to check for palindrome: A man, a plan, a canal: Panama

Output >> True


Process finished with exit code 0
```