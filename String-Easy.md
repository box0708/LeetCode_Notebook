> A:65 a:97 0:48

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
## 443. String Compression

> Given an array of characters, compress it in-place.

> The length after compression must always be smaller than or equal to the original array.

> Every element of the array should be a character (not int) of length 1.

> After you are done modifying the input array in-place, return the new length of the array.

1. In-place: two pointer, scan once.

2. Store the count the current char (```c = chars[i]```), determine the value of count, then update the ```char[result]```

```cpp
class Solution {
public:
    int compress(vector<char>& chars) {
        if (chars.size() <= 1){
            return chars.size();
        }
        
        char c = chars[0];
        int result=1, count=1;
        for (int i=1; i<chars.size(); i++){
            if (chars[i] == c){
                count++;
            }
            else{
                if (count>1){
                    string s = to_string(count);  
                    for (auto ch : s) {  
                        chars[result] = ch;
                        result++;
                    }
                }
                count=1;
                c = chars[i];
                chars[result++]=c;
            }
        }
        if (count>1){
            string s = to_string(count);  
            for (auto ch : s) {  
                chars[result] = ch;
                result++;
            }
        }
        chars.resize(result);
        return result;
    }
};
```

## 541. Reverse String II

1. the length of each step is ```2*k```

2. the usage of built-in ```reverse``` method
