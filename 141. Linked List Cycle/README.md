# 141. Linked List Cycle

Given head, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to. Note that pos is not passed as a parameter.

Return true if there is a cycle in the linked list. Otherwise, return false.

## Example

Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).

Input: head = [1,2], pos = 0
Output: true
Explanation: There is a cycle in the linked list, where the tail connects to the 0th node.

Input: head = [1], pos = -1
Output: false
Explanation: There is no cycle in the linked list.

## solution

1.遍历链表，把链表的元素添加到set中，如果node有重复，则为回环

2.遍历链表，2个指针A、B，A指针每步加1，B指针每步加2，如此循环。如果指针A、B相等，那么为回环

```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
 
    bool hasCycle(ListNode *head) {
       
        ListNode* fast = head;
        
        while(fast)
        {
            if(fast->next)
            {
                head = head->next;  
                fast = fast->next->next;
            }
            else
            {
                break;
            }
            
            if(fast == head)
            {
                return true;
            }
        }
        return false;
    }
```