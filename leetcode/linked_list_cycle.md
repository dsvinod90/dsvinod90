---
title: Linked List Cycle 
layout: default
filename: linked_list_cycle 
--- 
[back](/dsvinod90/leetcode)

# [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)
###### tags: `Leetcode`, `Easy`, `Linked List`

## Python Code
```python
"""
Approach: Linked List
Time Complexity: O(N)
Space Complexity: O(1)
"""

from typing import Optional


class ListNode:
    visited = set()

    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

    def __str__(self):
        if not self:
            return None
        if self not in self.visited:
            self.visited.add(self)
            return f"{self.val} -> {self.next}"
        else:
            return f"[{self.val}]"


class LinkedListCycle:
    def _has_cycle(self, head: Optional[ListNode]) -> bool:
        """ Return true/false for finding loops in the linked list
        Accept a linked list and return true if a cycle exists in the linked list and false otherwise
        :param head: ListNode that marks the beginning of the linked list
        :return: true/false based on the presence of a cycle in the linked list
        """

        # initialise slow and fast pointer to initially point at the head node
        tortoise, hare = head, head
        # iterate till the fast node has a next node
        while hare and hare.next:
            # slow points to the next node
            tortoise = tortoise.next
            # fast points to the node after the next
            hare = hare.next.next
            # if slow and fast are the same node then there is a cycle. Return true
            if tortoise == hare:
                return True
        # if the control reaches here then there were no cycles. Return false
        return False

    def process(self, node: Optional[ListNode]) -> None:
        print(f"\nOutput >> {self._has_cycle(node)}\n")


if __name__ == '__main__':
    node_hash = {"None": None}
    count = int(input("Enter the number of nodes in the linked list: "))
    print("Enter node values: ")
    for index in range(count):
        if index == 0:
            input_num = int(input(f"Enter the value for head node: "))
        else:
            input_num = int(input(f"Enter the value for node {index}: "))
        node_hash[index] = ListNode(input_num)
    for index in range(count):
        if index == 0:
            print("For head:")
        else:
            print(f"For node {index}:")
        nxt = input("\tEnter the next pointer: ")
        if nxt == "Head":
            nxt = 0
        elif nxt != "None":
            nxt = int(nxt)
        node_hash[index].next = node_hash[nxt]
    print(f"You have created the following linked list: {node_hash[0]}")
    LinkedListCycle().process(node_hash[0])
```

## Output
```shell
Enter the number of nodes in the linked list: 4
Enter node values: 
Enter the value for head node: 3
Enter the value for node 1: 2
Enter the value for node 2: 0
Enter the value for node 3: 4
For head:
	Enter the next pointer: 1
For node 1:
	Enter the next pointer: 2
For node 2:
	Enter the next pointer: 3
For node 3:
	Enter the next pointer: 1
You have created the following linked list: 3 -> 2 -> 0 -> 4 -> [2]

Output >> True


Process finished with exit code 0
```