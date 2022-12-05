---
title: Reverse Polish Notation
layout: default
filename: reverse_polish_notation 
--- 
[back](/dsvinod90/leetcode)

# [Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/)
###### tags: `Leetcode`, `Medium`, `Stack`

## Python Code
```python
from typing import List


class ReversePolishNotation:
    def _is_number(self, num: str) -> bool:
        """ Return true/false for string input
        Checks if the input string's contents is a valid integer value
        :param num: string input whose contents will be checked
        :return: True if the string contains a valid integer and False otherwise
        """

        return num.isdigit() or (num.startswith('-') and num[1:].isdigit())

    def _perform_operation(self, left: int, right: int, operator: str) -> int:
        """ Return integer after performing an arithmetic operation
        Performs basic arithmetic operation based on the input params
        :param left: integer to the left of the operator
        :param right: integer to the right of the operator
        :param operator: arithmetic operator
        :return: integer value obtained after performing the arithmetic operation
        """

        # addition
        if operator == '+':
            return left + right
        # subtraction
        elif operator == '-':
            return left - right
        # multiplication
        elif operator == '*':
            return left * right
        # division
        elif operator == "/":
            return int(left / right)

    def _eval_rpn(self, tokens: List[str]) -> int:
        """ Return the result after evaluating the input tokens
        Evaluates the tokens in reverse polish notation and gets the result of the evaulation
        :param tokens: List of strings containing numbers and basic arithmetic symbols
        :return: Integer after evaluating the tokens following the reverse polish notation
        """

        # initialize an empty stack
        stack = []
        # iterate through every token in the input list
        for token in tokens:
            # if the token is a valid integer then add it to the stack
            if self._is_number(token):
                stack.append(int(token))
            # if the token is not a valid integer then it should be an arithmetic operator
            else:
                # pop the last two elements from the stack
                right, left = int(stack.pop()), int(stack.pop())
                # perform the arithmetic operation on those two numbers based on the current token
                result = self._perform_operation(left, right, token)
                # append to the stack the result of the arithmetic operation
                stack.append(result)
        # the control will reach here after it has iterated through all the tokens in the input. Return the last value
        # of the stack
        return stack[-1]

    def process(self, input_tokens: List[str]) -> None:
        print(f"\nOutput >> {self._eval_rpn(input_tokens)}\n")


if __name__ == '__main__':
    count = int(input("Enter the number of tokens in the input list: "))
    input_tokens_list = []
    print("Enter the tokens: ")
    for _ in range(count):
        input_tokens_list.append(input())
    ReversePolishNotation().process(input_tokens_list)
```

## Output
```shell
Enter the number of tokens in the input list: 13
Enter the tokens: 
10
6
9
3
+
-11
*
/
*
17
+
5
+

Output >> 22
```