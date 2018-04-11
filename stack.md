## 496. Next Greater Element I

> You are given two arrays (without duplicates) nums1 and nums2 where nums1’s elements are subset of nums2. Find all the next greater numbers for nums1's elements in the corresponding places of nums2.
> 
> Input: nums1 = [4,1,2], nums2 = [1,3,4,2].
> 
> Output: [-1,3,-1]
> 
> Explanation:
> 
> For number 4 in the first array, you cannot find the next greater number for it in the second array, so output -1.
> 
> For number 1 in the first array, the next greater number for it in the second array is 3.
>   
> For number 2 in the first array, there is no next greater number for it in the second array, so output -1.

Note: the ```stack.pop()``` can store the 'break points' in the middle of traversing the array.

```cpp
class Solution {
public:
    vector<int> nextGreaterElement(vector<int>& findNums, vector<int>& nums) {
        stack<int> stk;
        unordered_map<int, int> mymap;
        
        for (int i=0; i<nums.size(); i++){
            // use while loop here to update all values in hash map of the left-hand side numbers.
            while (!stk.empty() && stk.top() < nums[i]){
                mymap[stk.top()] = nums[i];
                stk.pop();
            }
            stk.push(nums[i]);
        }
        
        vector<int> result(findNums.size());
        for (int i=0; i<findNums.size(); i++){
            if (mymap.find(findNums[i]) == mymap.end()) result[i] = -1;
            else result[i] = mymap[findNums[i]];
        }
        return result;
    }
};
```
