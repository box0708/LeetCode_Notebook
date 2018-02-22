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
