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
