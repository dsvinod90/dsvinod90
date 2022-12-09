---
title: Merge Two Sorted Lists
layout: default
filename: merge_two_sorted_lists 
--- 
[back](/dsvinod90/leetcode)

# [Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)
###### tags: `Leetcode`, `Easy`, `Linked List`

## Python Code
```python
"""
Approach: Linked List
Time Complexity: O(M+N)
Space Complexity: O(1)
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

class MergeTwoSortedLists:
    def _merge_two_lists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        """ Return the node that is the head of the merged linked list
        Take two input linked lists and merge them into one sorted linked list
        :param list1: head of the first linked list
        :param list2: head of the second linked list
        :return: node belonging to the merged sorted linked list
        """

        # declare and initialize an empty result node
        result = ListNode()
        # create a copy of result so that it can be used to return the output
        result_copy = result
        # iterate for the common number of nodes between the two linked lists
        while list1 and list2:
            # if the first list's value is lesser than the second's
            if list1.val < list2.val:
                # result points to list1's node
                result.next = list1
                # list1 points to its next node
                list1 = list1.next
            # if the second list's value is greater than or equal to the first's
            else:
                # result points to list2's node
                result.next = list2
                # list2 points to its next node value
                list2 = list2.next
            # result points to the next node
            result = result.next
        # if list1 is longer than list2 and there are remaining nodes of list1
        if list1:
            # add those nodes of list1 to the result
            result.next = list1
        # if list2 is longer than list1 and there are remaining nodes of list2
        elif list2:
            # add those nodes of list2 to the result
            result.next = list2
        # return the next node of result_copy. This is because the first node is an empty node.
        # We use result_copy because result now points to its last node.
        return result_copy.next

    def process(self, input_list1: Optional[ListNode], input_list2: Optional[ListNode]) -> None:
        print(f"\nOutput:\n\t{self._merge_two_lists(input_list1, input_list2)}\n")


if __name__ == '__main__':
    count1 = int(input("Enter the number of nodes in List 1: "))
    count2 = int(input("Enter the number of nodes in List 2: "))
    input_ll1, input_ll2 = ListNode(), ListNode(2)
    copy_ll1, copy_ll2 = input_ll1, input_ll2
    print("\nEnter the values for nodes of List 1: ")
    for index in range(count1):
        input_ll1.val = int(input(f"Enter the value of List 1, Node {index}: "))
        input_ll1.next = ListNode() if index < (count1 - 1) else None
        input_ll1 = input_ll1.next
    print("\nEnter the values for nodes of List 2: ")
    for index in range(count2):
        input_ll2.val = int(input(f"Enter the value of List 2, Node {index}: "))
        input_ll2.next = ListNode() if index < (count2 - 1) else None
        input_ll2 = input_ll2.next
    print("\nHere are the input linked lists: ")
    print(f"List1:\n\t{copy_ll1}")
    print(f"List2:\n\t{copy_ll2}")
    MergeTwoSortedLists().process(copy_ll1, copy_ll2)
```

## Output
```shell
Enter the number of nodes in List 1: 3
Enter the number of nodes in List 2: 3

Enter the values for nodes of List 1: 
Enter the value of List 1, Node 0: 1
Enter the value of List 1, Node 1: 2
Enter the value of List 1, Node 2: 4

Enter the values for nodes of List 2: 
Enter the value of List 2, Node 0: 1
Enter the value of List 2, Node 1: 3
Enter the value of List 2, Node 2: 4

Here are the input linked lists: 
List1:
	1 -> 2 -> 4 -> None
List2:
	1 -> 3 -> 4 -> None

Output:
	1 -> 1 -> 2 -> 3 -> 4 -> 4 -> None


Process finished with exit code 0
```