## 581. Shortest Unsorted Continuous Subarray
> Given an integer array, you need to find one continuous subarray that if you only sort this subarray in ascending order, then the whole array will be sorted in ascending order, too.
> You need to find the shortest such subarray and output its length.
```cpp
class Solution {
public:
    int findUnsortedSubarray(vector<int>& nums) {
        if (nums.size()<=1){
            return 0;
        }
        
        int start=-1, result=0;
        for (int i=1; i<nums.size(); i++)
        {
            if (nums[i] < nums[i-1]){ // i: the end of the unsorted subarray
                int j=i; // find the start of the unsorted array
                while(j>0 && nums[j]<nums[j-1]){
                    swap(nums[j], nums[j-1]);
                    j--;
                }
                if (start==-1 || start>j){
                    start = j; // update start when the unsorted array becomes longer
                }
                result = max(result, i-start+1);
            }
        }
        return result;
    }
};
```
