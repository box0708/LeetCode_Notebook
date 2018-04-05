## 190. Reverse Bits

> Reverse bits of a given 32 bits unsigned integer.
> 
> For example, given input 43261596 (represented in binary as 00000010100101000001111010011100), return 964176192 (represented in binary as 00111001011110000010100101000000).

Note: use ```n & 1 == 1``` to check the final digit of n.

> 00000001
> 
> 10010000   result: 0

```cpp
class Solution {
public:
    uint32_t reverseBits(uint32_t n) {
        uint32_t res = 0;
        for (int i=0; i<32; i++){
            if (n & 1 == 1){
                res = (res << 1) + 1;
            }
            else{
                res = res << 1;
            }
            n = n >> 1;
        }
        return res;
    }
};
```
