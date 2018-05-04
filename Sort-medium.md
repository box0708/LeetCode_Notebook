## 75. Sort Colors

> Given an array with n objects colored red, white or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white and blue.
> 
> Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.
> 
> Input: [2,0,2,1,1,0]
> 
> Output: [0,0,1,1,2,2]

Note: ```in-place```: two pointers, quick sort.

```cpp
class Solution {
public:
    void sortColors(vector<int>& nums) {
        if (nums.size()==0 || nums.size()==1) return;
        int left=0, right=nums.size()-1, i=0;
        while (i <= right){
            if (nums[i] == 0){
                swap(nums[i], nums[left]);
                i++;
                left++;
            }
            
            else if (nums[i] == 1) i++;
            
            else if (nums[i] == 2){
                swap(nums[i], nums[right]);
                // Do not change i here. nums[i] is in the correct place after being swapped.
                right--;
            }
        }   
    }
};
```
