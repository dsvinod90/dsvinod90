---
title: Koko Eating Bananas
layout: default
filename: koko_eating_bananas 
--- 
[back](/dsvinod90/leetcode)

# [Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/)
###### tags: `Leetcode`, `Medium`, `Binary Search`

## Python Code
```python
import math
from typing import List


class KokoEatingBananas:
    def _min_eating_speed(self, piles: List[int], h: int) -> int:
        """ Return the minimum value k to finish all piles within time h
        Calculates the minimum speed at which koko should eat bananas such that she can eat all the bananas in the
        piles before the guards arrive in time h
        :param piles: list of integers representing number of bananas in each pile
        :param h: integer representing the time for within which the piles of bananas should be finished
        :return: integer value that shows the minimum speed of eating bananas to successfully finish all the
        piles before time h
        """

        # declare and initialize left and right as 1 and the max value of the pile. This represents the range
        # of speed that koko can have to eat the bananas
        left, right = 1, max(piles)
        # declare and initialize result to have the maximum value
        result = right
        # loop over the speed range using binary search technique
        while left <= right:
            # find the mid-value for speed
            k = (left + right) // 2
            # declare and initialize the current total time to 0.
            # This is to keep track of the total time taken to finish the piles at the current speed
            curr_total_time = 0
            # iterate through the piles
            for pile in piles:
                # calculate total time taken to complete that pile at the current speed of k bananas per unit time
                curr_total_time += math.ceil(pile / k)
            # if the current total time is more than h, then it means that koko is eating at a slow pace.
            # She needs to speed up.
            if curr_total_time > h:
                # point left to the number just after mid
                left = k + 1
            # if the current total time is less than or equal to h, then it means that koko is eating at a fast pace.
            # She needs to slow down
            else:
                # point right to the number just before mid
                right = k - 1
                # result would be the minimum value of mid seen so far
                result = min(result, k)
        # At this point, result will have the least speed at which koko can finish eating the bananas
        # before the guards arrive in time h
        return result

    def process(self, input_piles: List[int], input_time: int) -> None:
        print(f"\nOutput >> {self._min_eating_speed(input_piles, input_time)}\n")


if __name__ == '__main__':
    count = int(input("Enter the number of piles of bananas: "))
    input_piles_list = []
    print("Enter the number of bananas for each pile: ")
    for _ in range(count):
        input_piles_list.append(int(input()))
    input_target_time = int(input("Enter the time after which guards will arrive: "))
    KokoEatingBananas().process(input_piles_list, input_target_time)
```

## Output
```shell
Enter the number of piles of bananas: 5
Enter the number of bananas for each pile: 
30
11
23
4
20
Enter the time after which guards will arrive: 5

Output >> 30


Process finished with exit code 0
```