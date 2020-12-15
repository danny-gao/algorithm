# 2. Add Two Numbers

## Example
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.

## solution
1.遍历 l1和l2，l1每个元素与l2每个元素相加，求出进位，让进位进入下一次循环。
  最后当 l1和l2遍历结束，再判断进位是否为0, 以添加最后一个节点

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


    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
       
        ListNode* ret = new ListNode();
        ListNode* head = ret;
        int sum = 0;
        int add = 0;
        
        while(l1 || l2)
        {
            sum = add;
            if(l1)
            {
                sum = sum + l1->val;
                l1 = l1->next;
            }
            
            if(l2)
            {
                sum = sum + l2->val;
                l2 = l2->next;
            }
                    
            ret->next = new ListNode(sum%10);
            ret = ret->next;
            add = sum/10;
            
        }
        
        if(add != 0)
        {
            ret->next = new ListNode(add);
        }
        return head->next;
    }
```