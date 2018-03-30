## 242. Valid Anagram

> Given two strings s and t, write a function to determine if t is an anagram of s.
> 
> For example,
> s = "anagram", t = "nagaram", return true.
> s = "rat", t = "car", return false.

The usage of Bit-map.

```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        if (s.size()==0 && t.size()==0) return true;
        if (s.size() == 0 || s.size() != t.size()) return false;
        int bitmap[26] = {0};
        
        for (int i=0; i<s.size(); i++){
            bitmap[int(s[i] - 'a')]++;
            bitmap[int(t[i] - 'a')]--;
        }
        
        for (int i=0; i<25; i++){
            if (bitmap[i] != 0){
                return false;
            }
        }
        
        return true;
    }
};
```
