# LeetCode记录
## 26. Remove duplicates from sorted array
两个指针，一个遍历数组，一个存储结果
```cpp
        if (nums.size() == 0) return 0;
        int i=1, current=1;
        for(i=1; i<nums.size(); i++)
        {
            if (nums[i-1] != nums[i])
            {
                #current ++;
                nums[current] = nums[i];
                current ++;
            }
        }
        return current;
```

## 27. Remove Element
读题。 顺序可变，只需要一个指针扫描，一个指针存储当前需要更改的位置。
> Given an array and a value, remove all instances of that value in-place and return the new length.
> Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.
> ***The order of elements can be changed. It doesn't matter what you leave beyond the new length.***

```cpp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        if (nums.size()==0) return 0; // check: null
        int result=0, i=0;
        for (i=0; i<nums.size(); i++)
        {
            if (nums[i] != val)
            {
                nums[result] = nums[i];
                result++;
            }
        }
        return result;
    }
};
```
## 83. Remove Duplicates from Sorted List 
Similar to 26.
> Given a sorted linked list, delete all duplicates such that each element appear only once.
> For example,
> Given 1->1->2, return 1->2.
> Given 1->1->2->3->3, return 1->2->3.

```cpp
class Solution {
public:
    ListNode* deleteDuplicates(ListNode* head) {
        ListNode* current = head;
        
        while(current)
        {
            while(current->next && current->val == current->next->val)
                current->next = current->next->next;
            current = current->next;
        }
        
        return head;
    }
};
```
## 141. Linked List Cycle
Fast and slow pointer.

## 160. Intersection of Two Linked Lists
Step 1: check-null?

Step 2: traverse to the end, store length, check-same end point?

Step 3: traverse from the same start point, check-same pointer?
