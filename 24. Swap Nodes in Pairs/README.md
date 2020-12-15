# 24. Swap Nodes in Pairs

Given a linked list, swap every two adjacent nodes and return its head.

You may not modify the values in the list's nodes. Only nodes itself may be changed.

## Example

Input: head = [1,2,3,4]
Output: [2,1,4,3]

Input: head = [1]
Output: [1]

Input: head = []
Output: []

## solution

1.遍历输入的链表，然后两两交换(交换值或者交换ListNode)

```
     ListNode* swapPairs(ListNode* head) {

        int value = 0;
        ListNode* pre = nullptr;
        ListNode* ret = head;
        while(head && head->next)
        {
            pre = head;
            head = head -> next;
            
            //swap val
            value = pre->val;
            pre->val = head->val;
            head->val = value;    
            
            head = head -> next;
                 
        }
        return ret;
    }
```