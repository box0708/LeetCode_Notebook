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

## 86. Partition List

> Given a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.
> 
> You should preserve the original relative order of the nodes in each of the two partitions.
> 
> Input: head = 1->4->3->2->5->2, x = 3
> 
> Output: 1->2->2->4->3->5

Note: create and maintain two linked lists. Iterate the original linked list and link the two sub-lists after iteration.

```cpp
class Solution {
public:
    ListNode* partition(ListNode* head, int x) {
        ListNode* p = new ListNode(-1);
        ListNode* phead = p;
        ListNode* q = new ListNode(-1);
        ListNode* qhead = q;
        
        ListNode* temp = head;
        while (temp != NULL){
            if (temp->val < x){
                ListNode* newnode = new ListNode(temp->val);
                p->next = newnode;
                p = p->next;
            }
            else{
                ListNode* newnode = new ListNode(temp->val);
                q->next = newnode;
                q = q->next;
            }
            temp = temp->next;
        }
        
        p->next = qhead->next;
        qhead->next = NULL;
        return phead->next;
    }
};
```
