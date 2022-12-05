---
title: Valid Parentheses 
layout: default
filename: valid_parentheses 
--- 
[back](/dsvinod90/leetcode)

# [Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)
###### tags: `Leetcode`, `Easy`, `Stack`

## Python Code
```python
"""
Approach: Stacks
Time Complexity: O(N)
Space Complexity: O(N)
"""

class ValidParentheses:
    # global hash map that maps closing brackets with their matching opening brackets
    BRACKET_MAP = {
        ')': '(',
        ']': '[',
        '}': '{'
    }

    def _is_valid(self, s: str) -> bool:
        # initialize an empty stack
        stack = []
        # iterate through every bracket of the input string
        for bracket in s:
            # two conditions for invalid parentheses:
            # 1. if stack is empty and string begins with a closing bracket
            # 2. if stack is not empty and the next bracket in the string is a closing bracket and the top element in
            # the stack is its corresponding opening bracket
            if ((bracket in self.BRACKET_MAP.keys() and not stack) or
                    (stack and bracket in self.BRACKET_MAP.keys() and self.BRACKET_MAP[bracket] != stack.pop())):
                return False
            # if next bracket is an opening bracket then add it to the stack
            elif bracket in self.BRACKET_MAP.values():
                stack.append(bracket)
        # if stack is empty, then all opening brackets have been closed in the right order and that it is a valid input
        return stack == []

    def process(self, input_string: str) -> None:
        print(f"\nOutput >> {self._is_valid(input_string)}\n")


if __name__ == '__main__':
    input_str = input("Enter the parentheses string: ")
    ValidParentheses().process(input_str)
```

## Output
```shell
Enter the parentheses string: {[]((){})}

Output >> True


Process finished with exit code 0
```