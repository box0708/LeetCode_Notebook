## 82. Remove Duplicates from Sorted List II

>  Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only ***distinct*** numbers from the original list.

Note: add a new helper node (new head node). The loop control. 

```cpp
class Solution {
public:
    ListNode* deleteDuplicates(ListNode* head) {
        if (head == NULL || head->next == NULL) return head;
        ListNode* helper = new ListNode(-1);
        helper->next = head;
        ListNode* prev = helper;
        ListNode* cur = head;
        while (cur != NULL && cur->next != NULL){
            if ( cur->val != cur->next->val){
                prev = prev->next;
                cur = cur->next;
                continue;
            }
            
            else if ( cur->val == cur->next->val){
                while (cur->next != NULL && cur->val == cur->next->val){
                    cur = cur->next;
                }
                prev->next = cur->next;
                cur = cur->next;
                continue;
            }
        }
        return helper->next;
    }
};
```
