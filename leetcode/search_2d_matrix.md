---
title: Search A 2D Matrix
layout: default
filename: search_2d_matrix 
--- 
[back](/dsvinod90/leetcode)

# [Search A 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix/)
###### tags: `Leetcode`, `Medium`, `Binary Search`

## Python Code
```python
"""
Approach: Binary Search
Time Complexity: O(log(MN)); M = number of rows, N = number of columns
Space Complexity: O(1)
"""

from typing import List


class Search2DMatrix:
    def _searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        """ Return True or False for searching a target in a matrix
        Searches for the target integer in an m x n matrix
        :param matrix: 2D matrix with integers
        :param target: integer to be searched for in the matrix
        :return: True of target is found in the matrix, False otherwise
        """

        # declare and initialize the number of rows and columns in the matrix
        rows, columns = len(matrix), len(matrix[0])
        # declare top and bottom pointers at the first and last row of the matrix
        top, bottom = 0, rows-1
        # loop over the rows of the matrix
        while top <= bottom:
            # find the mid-row
            mid_row = (bottom + top) // 2
            # check if the target value is in the range of values of the mid-row
            if matrix[mid_row][columns - 1] >= target >= matrix[mid_row][0]:
                # declare and initialize left and right pointers at the first and last columns of the matrix
                left, right = 0, columns - 1
                # iterate through the columns
                while left <= right:
                    # find the mid-column
                    mid_col = (right + left) // 2
                    # if the target value is found at the mid-row, mid-column cell then return True
                    if matrix[mid_row][mid_col] == target:
                        return True
                    # if target value is greater than mid-row, mid-column cell then narrow search to the right
                    if target > matrix[mid_row][mid_col]:
                        # point left to the column after mid
                        left = mid_col + 1
                    # if target value is less than the mid-row, mid-column cell then narrow search to the left
                    else:
                        # point right to the column before mid
                        right = mid_col - 1
                # if control reaches here then it means that the target was in the range of the values of this row but
                # could not be found in that particular row. So it cannot be found anywhere else in the matrix.
                return False
            # if target is greater than the largest value of the mid-row then narrow search to the bottom of the matrix
            elif target > matrix[mid_row][columns - 1]:
                # point top to the row after mid-row
                top = mid_row + 1
            # if target is lesser than the smallest value of the mid-row then narrow search to the top of the matrix
            else:
                # point bottom to the row before mid-row
                bottom = mid_row - 1

    def process(self, input_matrix: List[List[int]], input_target: int) -> None:
        print(f"\nOutput >> {self._searchMatrix(input_matrix, input_target)}\n")


if __name__ == '__main__':
    rows = int(input("Enter the number of rows of the matrix: "))
    columns = int(input("Enter the number of columns of the matrix: "))
    user_input_matrix = [[0 for _ in range(columns)] for _ in range(rows)]
    print("Enter the values in the matrix: ")
    for row in range(rows):
        for column in range(columns):
            user_input_matrix[row][column] = int(input(f"Enter the value for cell({row}, {column}): "))
    input_target_value = int(input("Enter the target value to be searched for in the matrix: "))
    Search2DMatrix().process(user_input_matrix, input_target_value)
```

## Output
```shell
Enter the number of rows of the matrix: 3
Enter the number of columns of the matrix: 4
Enter the values in the matrix: 
Enter the value for cell(0, 0): 1
Enter the value for cell(0, 1): 3
Enter the value for cell(0, 2): 5
Enter the value for cell(0, 3): 7
Enter the value for cell(1, 0): 10
Enter the value for cell(1, 1): 11
Enter the value for cell(1, 2): 16
Enter the value for cell(1, 3): 20
Enter the value for cell(2, 0): 23
Enter the value for cell(2, 1): 30
Enter the value for cell(2, 2): 34
Enter the value for cell(2, 3): 60
Enter the target value to be searched for in the matrix: 34

Output >> True


Process finished with exit code 0
```