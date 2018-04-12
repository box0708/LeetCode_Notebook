## 11. Container With Most Water

> Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.
> 
> Note: You may not slant the container and n is at least 2.

```result = max(result, min(height[start], height[end]) * (end-start));```

The volumn of a container only depends on the lower bound. 

```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        if (height.size() <= 1) return 0;
        int start=0, end=height.size()-1, result=-1;
        while (start < end){
            result = max(result, min(height[start], height[end]) * (end-start));
            if (height[start] > height[end]){
                end--;
            }
            else{
                start++;
            }
        }
        return result;
    }
};
```

## 15. 3Sum (K sum problems)

> Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.
> 
> Note: The solution set must not contain duplicate triplets.
> 
> > For example, given array S = [-1, 0, 1, 2, -1, -4],
> > 
> > A solution set is:
> > 
> > [
> >   [-1, 0, 1],
> > 
> >   [-1, -1, 2]
> > ]

Solution: sort the given array, and scan from the two ends.

```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> result;
        if (nums.size() < 3) return result;
        sort(nums.begin(), nums.end()); // sort the given array
        
        for (int i=0; i<nums.size()-2; i++){
            if (nums[i] > 0) break;
            if (i>0 && nums[i] == nums[i-1]) continue;
            
            vector<int> temp;
            int start = i+1, end = nums.size()-1;

            while (start < end){
                if (nums[start] + nums[end] > -nums[i]) end--;
                else if (nums[start] + nums[end] < -nums[i]) start++;
                
                else{
                    temp.push_back(nums[i]);
                    temp.push_back(nums[start]);
                    temp.push_back(nums[end]);
                    result.push_back(temp);
                    temp.erase(temp.begin(), temp.end()); // clean the memory.
                    
                    while (start < end && nums[start] == nums[start+1])
                        start++;
                    while (start < end && nums[end] == nums[end-1])
                        end--;
                    start++;
                    end--;
                }
            }
        }
        return result;
    }
};
```

## 31. Next Permutation

> Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.
> 
> If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).
> 
> The replacement must be in-place, do not allocate extra memory.
> 
> Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.
> 
> 1,2,3 → 1,3,2
> 
> 3,2,1 → 1,2,3
> 
> 1,1,5 → 1,5,1

Note: traverse from the end, find the position where ```nums[pos] > nums[pos-1] && nums[pos] < nums[pos+1]```.

```cpp
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        if (nums.size()==0 || nums.size()==1) return;
        
        int pos = nums.size()-1;
        while (pos>0 && nums[pos]<=nums[pos-1]) pos--; // find the pos
        
        if (pos == 0){
            sort(nums.begin(), nums.end());
        }
        else{
            int target = nums[pos-1];
            for (int i=nums.size()-1; i>pos-1; i--){
                if (nums[i] > target) {
                    nums[pos-1] = nums[i];
                    nums[i] = target;
                    break;
                }
            }
            //sort(nums.begin()+pos, nums.end());
            helper(nums, pos, nums.size()-1);
        }
    }
    // quick-sort
    void helper(vector<int>& nums, int start, int end){
        if (start < end){
            int i=start, j=end, temp = nums[start];
            while (i < j){
                while (i<j && nums[j] >= temp)
                    j--;
                if (i < j) {
                    nums[i] = nums[j];
                    i++;
                }
                while (i<j && nums[i] <= temp){
                    i++;
                }
                if (i < j) {
                    nums[j] = nums[i];
                    j--;
                }
                nums[i] = temp;
                helper(nums, start, i-1);
                helper(nums, i+1, end);
                return;
            }
        }
        return;
    }
};
```

## 33. Search in Rotated Sorted Array

> Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.
> 
> (i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).
> 
> You are given a target value to search. If found in the array return its index, otherwise return -1.
> 
> You may assume no duplicate exists in the array.

Note: 1. binary search. ```while (i <= j)``` 2. use binary search to handle the partly sorted array

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int i=0, j=nums.size()-1;
        while (i <= j){
            int mid = i + (j-i)/2;
            if (target == nums[mid]) return mid; // find the target
            if (nums[mid] > nums[j]){ // rotated, mid in the left-hand side part
                if (target >= nums[i] && target < nums[mid]) j = mid-1; // target in the left-hand side part(sorted)
                else i = mid+1; // target not in the sorted part
            }
            else if (nums[mid] < nums[i]){ // rotated, mid in the right-hand side part
                if (target <= nums[j] && target > nums[mid]) i = mid+1; // target in the right sorted part
                else j = mid-1; // target not in sorted part
            }
            else{ // without rotation
                if (target > nums[mid]) i = mid+1;
                else j = mid-1;
            }
        }
        return -1;
    }
};
```


