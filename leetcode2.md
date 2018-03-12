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
Use a windows to scan through the all array.
```cpp
        double sum = accumulate(nums.begin(), nums.begin()+k, 0), result=sum;
        for (int i=k; i<nums.size(); i++)
        {
            sum = sum + nums[i] - nums[i-k];
            result = max(result, sum);
        }
```

## 697. Degree of an Array
Use 3 hash map (unordered_map) to store the frequency, the minimun index and maximum index for nums[i]. Meanwhile, record the degree of the array. Then scan through the whole array to get the shortest sub-array.

## 746. Min Cost Climbing Stairs
> On a staircase, the i-th step has some non-negative cost cost[i] assigned (0 indexed).

> Once you pay the cost, you can either climb one or two steps. You need to find minimum cost to reach the top of the floor, and you can either start from the step with index 0, or the step with index 1.

Dynamtic programming. ```cpp dp[i] = min(dp[i-2]+cost[i-2], dp[i-1]+cost[i-1]); ```
```cpp
class Solution {
public:
    int minCostClimbingStairs(vector<int>& cost) {
        int length = cost.size()+1; // the terminal state, cost.size()+1
        int dp[length];
        
        dp[0] = 0;
        dp[1] = 0;
        
        for (int i=2; i<length; i++)
        {
            dp[i] = min(dp[i-2]+cost[i-2], dp[i-1]+cost[i-1]);
        }
        
        return dp[length-1];
    }
};
```

## 198. House Robber
Dynamic programming.

1. Find the equation.

2. The size of the ```dp``` vector.
