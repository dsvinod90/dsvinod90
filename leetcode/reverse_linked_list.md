---
title: Reverse Linked List
layout: default
filename: reversed_linked_list 
--- 
[back](/dsvinod90/leetcode)

# [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)
###### tags: `Leetcode`, `Easy`, `Linked List`

## Python Code
```python
"""
Approach: Linked List
Time Complexity: O(N)
Space Complexity: O(N)
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


class ReverseLinkedList:
    def _reverse_list(self, head: Optional[ListNode]) -> Optional[ListNode]:
        """ Return the reversed linked list
        Take as input a node which is the start of a linked list, reverse the linked list and return
        the head of the reversed list
        :param head: ListNode that marks the head of the linked list
        :return: ListNode of the head that is the reversed linked list
        """

        # base case: if head is None or head points to None (i.e. it is the last/only node) then return that head.
        if not head or not head.next:
            return head
        # recursively call this method
        reverse = self._reverse_list(head.next)
        # change the direction of the pointers
        head.next.next = head
        head.next = None
        # return the reversed list i.e. the ListNode which is the head of the reversed linked list
        return reverse

    def process(self, input_head: Optional[ListNode]) -> None:
        print(f"\nOutput:\n\t{self._reverse_list(input_head)}\n")


if __name__ == '__main__':
    count = int(input("Enter the number of nodes in the linked list: "))
    input_node = ListNode()
    copy_input = input_node
    for index in range(count):
        input_node.val = int(input(f"Enter value for Node {index}: "))
        input_node.next = ListNode() if index < (count - 1) else None
        input_node = input_node.next
    input_node = None
    print(f"\nProvided linked list:\n\t{copy_input}")
    ReverseLinkedList().process(copy_input)
```

## Output
```shell
Enter the number of nodes in the linked list: 5
Enter value for Node 0: 1
Enter value for Node 1: 2
Enter value for Node 2: 3
Enter value for Node 3: 4
Enter value for Node 4: 5

Provided linked list:
	1 -> 2 -> 3 -> 4 -> 5 -> None

Output:
	5 -> 4 -> 3 -> 2 -> 1 -> None


Process finished with exit code 0
```