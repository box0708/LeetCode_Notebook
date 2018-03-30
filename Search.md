## 475. Heaters

> Winter is coming! Your first job during the contest is to design a standard heater with fixed warm radius to warm all the houses.
> 
> Now, you are given positions of houses and heaters on a horizontal line, find out minimum radius of heaters so that all houses could be covered by those heaters.
> 
> So, your input will be the positions of houses and heaters seperately, and your expected output will be the minimum radius standard of heaters.

> Input: [1,2,3,4],[1,4]

> Output: 1

Do binary search for every house in ```heaters```. Find the two nearest (or one, for the boundary) heaters near the house.

```cpp
class Solution {
public:
    int findRadius(vector<int>& houses, vector<int>& heaters) {
        //sort(houses.begin(), houses.end());
        sort(heaters.begin(), heaters.end());
        int result = 0;
        
        for (int i=0; i<houses.size(); i++){
            int left=0, right=heaters.size();
            while(left < right){
                int mid = left + (right-left)/2;
                if (heaters[mid] < houses[i]) left = mid+1;
                else right = mid;
            }
            
            int pos_r, pos_l;
            if (right == heaters.size()) pos_r = INT_MAX;
            else pos_r = heaters[right] - houses[i];
            
            if (right == 0) pos_l = INT_MAX;
            else pos_l = houses[i]- heaters[right-1];
            
            result = max(result, min(pos_r, pos_l));
        }
        return result;
    }
};
```
