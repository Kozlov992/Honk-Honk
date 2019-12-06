# Dynamic programming

+ [Knapsack](#knapsack)
+ [Climbing Stairs](#climbing-stairs)
+ [Longest Increasing Subsequence](#longest-increasing-subsequence)
+ [Coin Change](#coin-change)
+ [Coin Change 2](#coin-change-2)
+ [House Robber](#house-robber)
+ [House Robber II](#house-robber-ii)
+ [Jump Game](#jump-game)
+ [Jump Game II](#jump-game-ii)
+ [Decode Ways](#decode-ways)
+ [Unique Paths](#unique-paths)
+ [Unique Paths II](#unique-paths-ii)
+ [Longest Common Subsequence](#longest-common-subsequence)
+ [Word Break](#word-break)
+ [N-Queens](#n-queens)
+ [N-Queens II](#n-queens-ii)

## Knapsack problem

https://stepik.org/lesson/13259/step/5?unit=3444

```C++

```

## Climbing Stairs

https://leetcode.com/problems/climbing-stairs/

```C++

```

## Longest Increasing Subsequence

https://leetcode.com/problems/longest-increasing-subsequence/

```C++

```

## Coin Change

https://leetcode.com/problems/coin-change/


```

## Coin Change 2

https://leetcode.com/problems/coin-change-2/

```C++

```

## House Robber

https://leetcode.com/problems/house-robber/

```C++
class Solution {
public:
    int rob(vector<int>& nums) {
        if (nums.size() == 0) 
            return 0;
        int prev1 = 0;
        int prev2 = 0;
        for (auto num : nums) {
            int tmp = prev1;
            prev1 = max(prev2 + num, prev1);
            prev2 = tmp;
        }
        return prev1;
    }
};
```

## House Robber II

https://leetcode.com/problems/house-robber-ii/

```C++
class Solution {
public:
    int rob(vector<int>& nums) {
        int n = nums.size(); 
        if (n == 0)
            return 0;
        if (n == 1)
            return nums[0];
        return max(rob(nums, 0, n - 2), rob(nums, 1, n - 1));
    }
    int rob(vector<int>& nums, int l, int r) {
        if (nums.size() == 0) 
            return 0;
        int prev1 = 0;
        int prev2 = 0;
        for (int i = l; i <= r; i++) {
            int tmp = prev1;
            prev1 = max(prev2 + nums[i], prev1);
            prev2 = tmp;
        }
        return prev1;
    }
};
```

## Jump Game

https://leetcode.com/problems/jump-game/

```C++

```

## Jump Game II

https://leetcode.com/problems/jump-game-ii/

```C++

```

## Decode Ways

https://leetcode.com/problems/decode-ways/

```C++

```

## Unique Paths

https://leetcode.com/problems/unique-paths/

```C++

```

## Unique Paths II

https://leetcode.com/problems/unique-paths-ii/

```C++

```

## Longest Common Subsequence

https://leetcode.com/problems/longest-common-subsequence/

```C++

```

## Word Break

https://leetcode.com/problems/word-break/

```C++
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        if (wordDict.size() == 0)
            return false;
        unordered_set<string> dict(wordDict.begin(), wordDict.end());
        vector<bool> isValidSubString (s.size() + 1, false);
        isValidSubString[0] = true;
        for (int i = 1; i <= s.size(); i++)
            for (int j = i - 1; j >= 0; j--)
                if (isValidSubString[j]) {
                    string word = s.substr(j, i - j);
                    if (dict.find(word) != dict.end()) {
                        isValidSubString[i] = true;
                        break;
                    }
                }
        return isValidSubString[s.size()];
    }
};
```

## N-Queens

https://leetcode.com/problems/n-queens/

```C++

```

## N-Queens II

https://leetcode.com/problems/n-queens-ii/

```C++

```
