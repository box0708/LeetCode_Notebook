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
