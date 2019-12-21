```C++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        vector<int> dict(256, -1);
        int maxstr = 0, start = -1;
        for (int i = 0; i < s.length(); i++) {
            if (dict[s[i]] > start)
                start = dict[s[i]];
            dict[s[i]] = i;
            maxstr = max(maxstr, i - start);
        }
        return maxstr;
    }
};
```
```C++
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        if(nums.empty())   return 0;
        int curMax = nums[0], curMin = curMax, maxProduct = curMax;    
        for(int i = 1; i < nums.size(); ++i) {
            int p1 = curMax * nums[i];
            int p2 = curMin * nums[i];
            curMax = max(nums[i], max(p1, p2));
            curMin = min(nums[i], min(p1, p2));
            maxProduct = curMax > maxProduct ? curMax : maxProduct;
        }
        return maxProduct;
    }
};
```
