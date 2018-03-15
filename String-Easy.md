## 58. Length of Last Word

> Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word in the string.

> If the last word does not exist, return 0.

> Note: A word is defined as a character sequence consists of non-space characters only.

1. SPACE may occur in any position.

2. Scan from the end of string, find the end of last word.

3. Scan until the start of last word. (another SPACE), count, return.

## 67. Add Binary

***important***

```cpp
class Solution {
public:
    string addBinary(string a, string b) {
        int i=a.size()-1, j=b.size()-1, temp=0;
        string result(max(i,j)+1, '0');
        int carry=0;
        
        while(i>=0 || j>=0){
            temp = carry + (i>=0? a[i]-'0': 0) + (j>=0 ? b[j]-'0' : 0);
            if (temp>=2){
                carry = 1;
            }
            else{
                carry = 0;
            }
            result[max(i, j)] = temp%2 + '0';
            i--;
            j--;
        }
        
        if (carry == 1){
            result = "1" + result;
        }
        
        return result;
    }
};
```
