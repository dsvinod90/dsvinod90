---
title: Add Two Numbers
layout: default
filename: add_two_numbers 
--- 
[back](/dsvinod90/leetcode)

# [Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)
###### tags: `Leetcode`, `Medium`, `Linked List`

## Python Code
```python
"""
Approach: Linked List
Time Complexity: O(max(M,N))
Space Complexity: O(max(M,N))
"""

from typing import Optional


class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

    def __str__(self):
        if not self:
            return None
        return f"{self.val} -> {self.next}"


class AddTwoNumbers:
    def _add_two_numbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        """ Return a linked list which is the sum of the two input linked lists
        Accept two linked lists as input and return a linked list after summing the values of the input lists from left
        to right.
        :param l1: Fist ListNode input
        :param l2: Second ListNode input
        :return: Resulting LinkedList which is the sum of l1 and l2
        """

        # declare and initialize carry to be 0
        carry = 0
        # create a pre_result & result LinkedList
        pre_result = ListNode()
        result = pre_result
        # iterate through l1 and l2 until we reach the end of the longer one
        while l1 or l2:
            # num1 represents value of current head at l1 and num2 represents value of current head at l2
            num1, num2 = 0, 0
            # check if l1 is not None i.e. we have not reached the end of l1
            if l1:
                # assign node value to num1
                num1 = l1.val
                # point to the next node of l1
                l1 = l1.next
            # check if l2 is not None i.e. we have not reached the end of l2
            if l2:
                # assign node value to num2
                num2 = l2.val
                # point to the next node of l2
                l2 = l2.next
            # sum num1, num2 and carry; div will be stored in carry and mod will be stored as current sum
            carry, cur_sum = divmod(num1 + num2 + carry, 10)
            # assign current sum to the next node value of pre_result
            pre_result.next = ListNode(cur_sum)
            # point pre_result to the newly created node
            pre_result = pre_result.next
        # at this point all values of the nodes in the two input lists have been added. If any carry is left over, we
        # add it to the new node of pre_result
        if carry > 0:
            pre_result.next = ListNode(carry)
        # result still points to the first node of pre_result. Return the next node as that is the start of the
        # resulting linked list
        return result.next

    def process(self, input_list1: Optional[ListNode], input_list2: Optional[ListNode]) -> None:
        print(f"\nOutput:\n\t{self._addTwoNumbers(input_list1, input_list2)}\n")


if __name__ == '__main__':
    input_l1, input_l2 = ListNode(), ListNode()
    copy_l1, copy_l2 = input_l1, input_l2
    count1 = int(input("Enter number of nodes in l1: "))
    print("For List1: ")
    for index in range(count1):
        input_l1.val = int(input(f"Enter the value of node {index + 1}: "))
        input_l1.next = ListNode() if index < (count1 - 1) else None
        input_l1 = input_l1.next
    count2 = int(input("\nEnter number of nodes in l2: "))
    print("For List2: ")
    for index in range(count2):
        input_l2.val = int(input(f"Enter the value of node {index + 1}: "))
        input_l2.next = ListNode() if index < (count2 - 1) else None
        input_l2 = input_l2.next
    print(f"Here are the two input linked lists: \n"
          f"\tList1: {copy_l1}\n"
          f"\tList2: {copy_l2}\n")
    AddTwoNumbers().process(copy_l1, copy_l2)
```

## Output
```shell
Enter number of nodes in l1: 3
For List1: 
Enter the value of node 1: 2
Enter the value of node 2: 4
Enter the value of node 3: 3

Enter number of nodes in l2: 3
For List2: 
Enter the value of node 1: 5
Enter the value of node 2: 6
Enter the value of node 3: 4
Here are the two input linked lists: 
	List1: 2 -> 4 -> 3 -> None
	List2: 5 -> 6 -> 4 -> None


Output:
	7 -> 0 -> 8 -> None


Process finished with exit code 0
```