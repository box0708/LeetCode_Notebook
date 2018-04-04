## 91. Decode Ways

> A message containing letters from A-Z is being encoded to numbers using the following mapping:
> 
> 'A' -> 1
> 'B' -> 2
> ...
> 'Z' -> 26
> 
> Given an encoded message containing digits, determine the total number of ways to decode it.
> 
> For example:
> 
> Given encoded message "12", it could be decoded as "AB" (1 2) or "L" (12).
> 
> The number of ways decoding "12" is 2.

Note: the setting of loop.

```cpp
class Solution {
public:
    int numDecodings(string s) {
        //dp[n] = dp[n-1] + dp[n-2]
        if (s.size() == 0) return s.size();
        int dp[s.size()+1] = {0};
        dp[0] = 1;
        
        for (int i=0; i<s.size(); i++){
            if (s[i] != '0') dp[i+1] += dp[i];
            
            if (i>0 && checktwo(s[i-1], s[i])) dp[i+1] += dp[i-1];
        }
        return dp[s.size()];
    }
    
    bool checktwo (char a, char b){
        if (a == '0') return false;
        int number = (a - '0')*10 + (b - '0');
        return (number <= 26);
    }
};
```

## 96. Unique Binary Search Trees

> Given n, how many structurally unique BST's (binary search trees) that store values 1...n?

Note: ```dp[i] += dp[j] * dp[i-j-1];``` dp[i] += sum(possibile_left * possibile_right)

```cpp
class Solution {
public:
    int numTrees(int n) {
        if (n <= 0) return 0;
        int dp[n+1] = {0};
        dp[0] = 1;
        dp[1] = 1;
        for (int i=2; i<=n; i++){
            for (int j=0; j<i; j++){
                dp[i] += dp[j] * dp[i-j-1];
            }
        }
        return dp[n];
    }
};
```

## 139. Word Break

> Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, determine if s can be segmented into a space-separated sequence of one or more dictionary words. You may assume the dictionary does not contain duplicate words.
> 
> For example, given
> s = "leetcode",
> dict = ["leet", "code"].
> 
> Return true because "leetcode" can be segmented as "leet code".


> 
>  ```i: 0  1   2   3   4   5   6   7   8```
> 
>        l | e | e | t | c | o | d | e
> 
>                j       i |
> 
>                check 'etc'

```cpp
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        if (s.size() == 0 || wordDict.size() == 0) return false;
        
        bool dp[s.size()+1] = {false};
        dp[0] = true;
        
        for (int i=1; i<=s.size(); i++){
            for (int j=0; j<i; j++){
                string temp = s.substr(j, i-j);
                for (int index=0; index<wordDict.size(); index++){
                    if (dp[j] && wordDict[index] == temp){
                        dp[i] = true;
                        break;
                    }
                }
            }
        }
        return dp[s.size()];
    }
};
```


## 152. Maximum Product Subarray

> Find the contiguous subarray within an array (containing at least one number) which has the largest product.
> 
> For example, given the array [2,3,-2,4],
> the contiguous subarray [2,3] has the largest product = 6.


Note: ```+ * +``` and ```- * -```, store the maximum(positive) and minimum(negative), compare and update them once visit a number(shall I choose a new start for DP?)

```cpp
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        if (nums.size() == 1) return nums[0];
        
        int max_mul=nums[0], min_mul=nums[0], result=nums[0];
        
        for (int i=1; i<nums.size(); i++){
            int a = max_mul * nums[i];
            int b = min_mul * nums[i];
            max_mul = max(max(a,b), nums[i]);
            min_mul = min(min(a,b), nums[i]);
            result = max(max_mul, result);
        }
        return result;
    }
};
```
