---
title: Daily Temperatures
layout: default
filename: daily_temperatures 
--- 
[back](/dsvinod90/leetcode)

# [Daily Temperatures](https://leetcode.com/problems/daily-temperatures/)
###### tags: `Leetcode`, `Medium`, `Stack`

## Python Code
```python
"""
Approach: Stacks
Time Complexity: O(N)
Space Complexity: O(N)
"""

from typing import List


class DailyTemperatures:
    def _daily_temperatures(self, temperatures: List[int]) -> List[int]:
        """ Return list of days after which higher temp is expected
        Calculates the number of days after which the temperature might be higher than current date for every day in
        the input list
        :param temperatures: integer value representing temperature for a certain day
        :return: List of integers showing the number of days after which temperature might be higher
        """

        # declare and initialize result list with 0 values
        result = [0] * len(temperatures)
        # declare and initialize empty stack
        stack = []
        # iterate through every temperature reading of days
        for index, temp in enumerate(temperatures):
            # until the current temp is more than the previously added temp to the stack
            while stack and temp > stack[-1][0]:
                # calculate the diff of the index values of current temp and the last temp reading in the stack
                result[stack[-1][1]] = index - stack[-1][1]
                # remove the last added temp to the stack
                stack.pop()
            # add the current temp and index to the stack after removing all the other temps lower in value than
            # the current one
            stack.append((temp, index))
        # return the result list
        return result

    def process(self, input_temps: List[int]) -> None:
        print(f"\nOutput >> {self._daily_temperatures(input_temps)}\n")


if __name__ == '__main__':
    count = int(input("Enter the number of temperature readings: "))
    input_temp_list = []
    print("Enter the temparatures: ")
    for _ in range(count):
        input_temp_list.append(int(input()))
    DailyTemperatures().process(input_temp_list)
```

## Output
```shell
Enter the number of temperature readings: 8
Enter the temparatures: 
73
74
75
71
69
72
76
73

Output >> [1, 1, 4, 2, 1, 1, 0, 0]


Process finished with exit code 0
```