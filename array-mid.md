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
> >
> >   [-1, 0, 1],
> > 
> >   [-1, -1, 2]
> > 
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
