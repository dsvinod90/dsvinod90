---
title: Valid Sudoku
layout: default
filename: valid_sudoku 
--- 
[back](/dsvinod90/leetcode)

# [Valid Sudoku](https://leetcode.com/problems/valid-sudoku/)
###### tags: `Leetcode`, `Medium`, `Arrays and Hashing`

## Python Code
```python
"""
Approach: Arrays and Hashing
Time Complexity: O(N^2)
Space Complexity: O(N^2)
"""

from collections import defaultdict
from typing import List


class ValidSudoku:
    def _is_valid_sudoku(self, board: List[List[str]]) -> bool:
        # initialize rows, cols and boxes to be dictionaries with values as set
        rows, cols, boxes = defaultdict(set), defaultdict(set), defaultdict(set)
        # iterate through every row of the board
        for row in range(9):
            # iterate through every column of the board
            for col in range(9):
                # get the value of that cell on the board
                value = board[row][col]
                # skip if value is not a number
                if value == '.':
                    continue
                # check if value exists in rows, cols or boxes
                if (value in rows[row] or
                        value in cols[col] or
                        value in boxes[(row//3, col//3)]):
                    # if present, return False
                    return False
                # if value does not exist then add to rows, cols and boxes
                rows[row].add(value)
                cols[col].add(value)
                boxes[(row//3, col//3)].add(value)
        # if control reaches here then every row, column and box has non-repetitive digits
        return True

    def process(self, input_board: List[List[str]]) -> None:
        print(f"\nOutput >> {self._is_valid_sudoku(input_board)}\n")


if __name__ == '__main__':
    size = 9
    input_sudoku_board = [["." for _ in range(size)] for _ in range(size)]
    for r in range(size):
        for c in range(size):
            v = input(f"Enter number at position ({r}, {c}): ")
            if not v:
                continue
            else:
                input_sudoku_board[r][c] = v
    print("\nYour board is as follows:")
    for r in range(size):
        for c in range(size):
            print(input_sudoku_board[r][c], end="\t")
        print()
    ValidSudoku().process(input_sudoku_board)
```

## Output
```shell
Enter number at position (0, 0): 5
Enter number at position (0, 1): 3
Enter number at position (0, 2): 
Enter number at position (0, 3): 
Enter number at position (0, 4): 7
Enter number at position (0, 5): 
Enter number at position (0, 6): 
Enter number at position (0, 7): 
Enter number at position (0, 8): 
Enter number at position (1, 0): 6
Enter number at position (1, 1): 
Enter number at position (1, 2): 
Enter number at position (1, 3): 1
Enter number at position (1, 4): 9
Enter number at position (1, 5): 5
Enter number at position (1, 6): 
Enter number at position (1, 7): 
Enter number at position (1, 8): 
Enter number at position (2, 0): 
Enter number at position (2, 1): 9
Enter number at position (2, 2): 8
Enter number at position (2, 3): 
Enter number at position (2, 4): 
Enter number at position (2, 5): 
Enter number at position (2, 6): 
Enter number at position (2, 7): 6
Enter number at position (2, 8): 
Enter number at position (3, 0): 8
Enter number at position (3, 1): 
Enter number at position (3, 2): 
Enter number at position (3, 3): 
Enter number at position (3, 4): 6
Enter number at position (3, 5): 
Enter number at position (3, 6): 
Enter number at position (3, 7): 
Enter number at position (3, 8): 3
Enter number at position (4, 0): 4
Enter number at position (4, 1): 
Enter number at position (4, 2): 
Enter number at position (4, 3): 8
Enter number at position (4, 4): 
Enter number at position (4, 5): 3
Enter number at position (4, 6): 
Enter number at position (4, 7): 
Enter number at position (4, 8): 1
Enter number at position (5, 0): 7
Enter number at position (5, 1): 
Enter number at position (5, 2): 
Enter number at position (5, 3): 
Enter number at position (5, 4): 2
Enter number at position (5, 5): 
Enter number at position (5, 6): 
Enter number at position (5, 7): 
Enter number at position (5, 8): 6
Enter number at position (6, 0): 
Enter number at position (6, 1): 6
Enter number at position (6, 2): 
Enter number at position (6, 3): 
Enter number at position (6, 4): 
Enter number at position (6, 5): 
Enter number at position (6, 6): 2
Enter number at position (6, 7): 8
Enter number at position (6, 8): 
Enter number at position (7, 0): 
Enter number at position (7, 1): 
Enter number at position (7, 2): 
Enter number at position (7, 3): 4
Enter number at position (7, 4): 1
Enter number at position (7, 5): 9
Enter number at position (7, 6): 
Enter number at position (7, 7): 
Enter number at position (7, 8): 5
Enter number at position (8, 0): 
Enter number at position (8, 1): 
Enter number at position (8, 2): 
Enter number at position (8, 3): 
Enter number at position (8, 4): 8
Enter number at position (8, 5): 
Enter number at position (8, 6): 
Enter number at position (8, 7): 7
Enter number at position (8, 8): 9

Your board is as follows:
5	3	.	.	7	.	.	.	.	
6	.	.	1	9	5	.	.	.	
.	9	8	.	.	.	.	6	.	
8	.	.	.	6	.	.	.	3	
4	.	.	8	.	3	.	.	1	
7	.	.	.	2	.	.	.	6	
.	6	.	.	.	.	2	8	.	
.	.	.	4	1	9	.	.	5	
.	.	.	.	8	.	.	7	9	

Output >> True


Process finished with exit code 0
```