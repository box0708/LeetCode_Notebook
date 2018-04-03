## 91. Decode Ways

> A message containing letters from A-Z is being encoded to numbers using the following mapping:
> 
> 'A' -> 1
> 'B' -> 2
> ...
> 'Z' -> 26
> Given an encoded message containing digits, determine the total number of ways to decode it.
> 
> For example,
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
