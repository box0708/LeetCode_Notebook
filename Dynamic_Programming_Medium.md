## 91. Decode Ways

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
