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

## 605 Can Place Flowers
Find the continuous 0s. Use the built in methods of C++ vector, insert 0 into the begin and the end of the given vector, than scan the vector.

## 628. Maximum Product of Three Numbers
> Given an integer array, find three numbers whose product is maximum and output the maximum product.
Find the 3 biggest numbers and 2 smallest numbers.

## 643. Maximum Average Subarray I
1. Use a windows to scan through the all array.
2. 
```double sum = accumulate(nums.begin(), nums.begin()+k, 0), result=sum;
        for (int i=k; i<nums.size(); i++)
        {
            sum = sum + nums[i] - nums[i-k];
            result = max(result, sum);
        }
```
