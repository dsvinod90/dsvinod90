---
title: Min Stack
layout: default
filename: min_stack 
--- 
[back](/dsvinod90/leetcode)

# [Min Stack](https://leetcode.com/problems/min-stack/)
###### tags: `Leetcode`, `Medium`, `Stack`

## Python Code
```python
"""
Approach: Stacks
Time Complexity for each method: O(1)
"""

from typing import Tuple


class MinStack:

    def __init__(self):
        """Initializer
        Declare and initialize an empty stack
        """

        self.stack = []

    def print_menu(self):
        """ Print menu of commands
        Prints the codes for performing specific functions so that the user can choose accordingly
        :return: None
        """

        print("Your options are as follows:\n"
              "\t1 - Push to stack\n"
              "\t2 - Pop from stack\n"
              "\t3 - Show top element in the stack\n"
              "\t4 - Get min element of the stack\n"
              "\t5 - Print menu\n"
              "\t6 - Quit\n")

    def _top(self) -> Tuple:
        """ Return the last added tuple to the stack
        Private method to get the top element of the stack.
        :return: Tuple with first element as the value at that index and second element as the minimum element at
        that index position
        """

        return self.stack[-1]

    def push(self, val: int) -> None:
        """ Push to stack
        Push an integer to the stack
        :param val: Value to be pushed to the stack
        :type val: int
        :return: None
        """

        # calculate the current minimum value in the stack including the current element
        curr_min = min(val, self.get_min()) if self.stack else val
        # append the value and curr_min tuple to the stack
        self.stack.append((val, curr_min))

    def pop(self) -> None:
        """ Pop from stack
        Removes the last added element from the stack
        :return: None
        """

        self.stack.pop()

    def top(self) -> int:
        """ Return top value
        Gets the last inserted value to the stack
        :return: integer that was last added to the stack
        """

        return self._top()[0]

    def get_min(self) -> int:
        """ Return minimum value of the stack
        Gets the least value that was inserted into the stack at the time this method was called
        :return: integer that is the least in value in the stack
        """

        return self._top()[1]


if __name__ == '__main__':
    min_stack_obj = MinStack()
    min_stack_obj.print_menu()
    exit_loop = False
    while not exit_loop:
        choice = input("Enter your choice: ")
        if choice == '1':
            print("You have chosen to push to stack.")
            number = int(input("Enter an integer to be pushed to the stack: "))
            min_stack_obj.push(number)
        elif choice == '2':
            print("You have chosen to pop from stack.")
            min_stack_obj.pop()
            print("Popped last element from stack.")
        elif choice == '3':
            print(f"You have chosen to display the top element of the stack. It is {min_stack_obj.top()}")
        elif choice == '4':
            print(f"You have chosen to display the minimum element of the stack. It is {min_stack_obj.get_min()}")
        elif choice == '5':
            min_stack_obj.print_menu()
        elif choice == '6':
            exit_loop = True
            print("Terminating execution ... ")
        else:
            print("Invalid choice. Please refer to the menu below.")
            min_stack_obj.print_menu()
```

## Output
```shell
Your options are as follows:
	1 - Push to stack
	2 - Pop from stack
	3 - Show top element in the stack
	4 - Get min element of the stack
	5 - Print menu
	6 - Quit

Enter your choice: 1
You have chosen to push to stack.
Enter an integer to be pushed to the stack: -2
Enter your choice: 1
You have chosen to push to stack.
Enter an integer to be pushed to the stack: 0
Enter your choice: 1
You have chosen to push to stack.
Enter an integer to be pushed to the stack: -3
Enter your choice: 4
You have chosen to display the minimum element of the stack. It is -3
Enter your choice: 2
You have chosen to pop from stack.
Popped last element from stack.
Enter your choice: 3
You have chosen to display the top element of the stack. It is 0
Enter your choice: 4
You have chosen to display the minimum element of the stack. It is -2
Enter your choice: 6
Terminating execution ... 

Process finished with exit code 0
```