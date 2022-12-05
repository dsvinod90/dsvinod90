---
title: Car Fleet
layout: default
filename: car_fleet 
--- 
[back](/dsvinod90/leetcode)

# [Car Fleet](https://leetcode.com/problems/car-fleet/)
###### tags: `Leetcode`, `Medium`, `Stack`

## Python Code
```python
"""
Approach: Stacks
Time Complexity: O(N.log(N))
Space Complexity: O(N)
"""

from typing import List


class CarFleet:
    def _car_fleet(self, target: int, position: List[int], speed: List[int]) -> int:
        """ Return number of fleets reaching the target
        Calculates the number of fleets that will reach the destination based on the position and speed of the cars
        :param target: integer value representing the destination of the fleet
        :param position: list of integer values representing the positions of every car in the fleet
        :param speed: list of integer values representing the speed of the car at every index position
        :return: integer representing the number of fleets reaching the destination
        """

        # map position and speed from the two lists
        pos_speed_map = list(zip(position, speed))
        # sort the mapped list in reverse order of the car's positions such that the first car is the one
        # closest to the destination
        pos_speed_map.sort(reverse=True)
        # declare and initialize an empty stack which will help keep track of the number of fleets
        # reaching the destination
        stack = []
        # iterate through the mapped list
        for pos, speed in pos_speed_map:
            # calculate the time taken for the car at current position to reach the destination
            time = (target - pos) / speed
            # append this time to the stack
            stack.append(time)
            # if the time at the last position in the stack is less than the one before that then pop the last element.
            # this is because the car with less time will eventually catch up with the slower car and then continue
            # the rest of the journey with that speed
            if len(stack) >= 2 and stack[-1] <= stack[-2]:
                stack.pop()
        # the length of the stack represents the number of fleets arriving at the destination
        return len(stack)

    def process(self, input_target: int, input_position: List[int], input_speed: List[int]) -> int:
        print(f"\nOutput >> {self._car_fleet(input_target, input_position, input_speed)}\n")


if __name__ == '__main__':
    count = int(input("Enter the number of cars in the fleet: "))
    input_target_value = int(input("Enter the target: "))
    input_position_list, input_speed_list = [], []
    print("Enter the positions: ")
    for _ in range(count):
        input_position_list.append(int(input()))
    print("Enter the speeds: ")
    for _ in range(count):
        input_speed_list.append(int(input()))
    CarFleet().process(input_target_value, input_position_list, input_speed_list)
```

## Output
```shell
Enter the number of cars in the fleet: 5
Enter the target: 12
Enter the positions: 
10
8
0
5
3
Enter the speeds: 
2
4
1
1
3

Output >> 3
```