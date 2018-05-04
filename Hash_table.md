## 3. Longest Substring Without Repeating Characters

> Given a string, find the length of the longest substring without repeating characters.
> 
> Examples:
> 
> Given "abcabcbb", the answer is "abc", which the length is 3.
> 
> Given "bbbbb", the answer is "b", with the length of 1.
> 
> Given "pwwkew", the answer is "wke", with the length of 3. Note that the answer must be a substring, "pwke" is a subsequence and not a substring.

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        if (s.size() <= 1) return s.size();
        
        vector<int> dict(256, -1); // array won't work and I don't know why.
        int start=-1, result=0;
        for (int i=0; i<s.size(); i++){
            if (dict[s[i]] > start){ // s[i] has appeared before
                start = dict[s[i]]; // update the start point: the position where s[i] occured last time.
            }
            dict[s[i]] = i;
            result = max(result, i-start);
        }
        return result;
    }
};
```
