---
title: Generate Parentheses
layout: default
filename: generate_parentheses 
--- 
[back](/dsvinod90/leetcode)

# [Generate Parentheses](https://leetcode.com/problems/generate-parentheses/)
###### tags: `Leetcode`, `Medium`, `Stack`

## Python Code
```python
"""
Approach: Stacks
Time Complexity: O(4^N / N^(1/2))
Space Complexity: O(4^N / N^(1/2))
"""

from typing import List


class GenerateParentheses:
    def _generate_parentheses(self, n: int) -> List[str]:
        """ Return a list of all possible combinations of parentheses
        Takes as input an integer value representing the number of pairs of parentheses and returns a list of all
        possible combinations of valid parentheses that can exist
        :param n: integer value for the number of pairs of parentheses
        :return: List of all possible combinations of parentheses for n pairs
        """

        # declare and initialize empty lists for result and stack
        result, stack = [], []

        def backtrack(opened, closed):
            """ Backtracking to find all combinations of parentheses
            Recursive backtracking to find all valid combinations of parentheses
            :param opened: integer value to keep track of the number of opened parentheses
            :param closed: integer value to keep track of the number of closed parentheses
            :return: None
            """

            # if number of opened and closed parentheses are equal
            if opened == closed == n:
                # join all the elements of stack and create a string of parentheses and append to result list
                result.append("".join(stack))
                # exit the method because the base case has reached
                return
            # if opened brackets are less than the input value 'n'
            if opened < n:
                # add an open bracket to the stack
                stack.append("(")
                # recursively call backtrack method incrementing the value of opened bracket
                backtrack(opened + 1, closed)
                # remove the added open bracket from the stack
                stack.pop()
            # closed brackets should be equal in count to the open brackets
            # if closed brackets are less than the open brackets
            if closed < opened:
                # add a closed bracket to the stack
                stack.append(")")
                # recursively call backtrack method incrementing the value of closed bracket
                backtrack(opened, closed + 1)
                # remove the added closed bracket from the stack
                stack.pop()

        # start the backtracking with 0 open and 0 closed brackets
        backtrack(0, 0)
        # return the result list
        return result

    def process(self, pairs: int) -> None:
        print(f"\nOutput >> {self._generate_parentheses(pairs)}\n")


if __name__ == '__main__':
    input_pairs = int(input("Enter the number of pairs of parentheses: "))
    GenerateParentheses().process(input_pairs)
```

## Output
```shell
Enter the number of pairs of parentheses: 3

Output >> ['((()))', '(()())', '(())()', '()(())', '()()()']


Process finished with exit code 0
```