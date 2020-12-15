# 206. Reverse Linked List

Reverse a singly linked list.


## Example

Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL

## solution

1.

```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* pre = NULL;
        ListNode* next = NULL;
        
        while(head)
        {
			//做交换
            next = head->next;
            head->next = pre;
            pre = head;
            head = next;
        }
        
        return pre;
    }
};
```