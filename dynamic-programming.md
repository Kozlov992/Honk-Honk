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
#include <iostream>
#include <vector>
using namespace std;
int main() {
  int capacity, n, value;
  cin >> capacity >> n;
  vector<vector<int>> maxValue(n + 1, vector<int>(capacity + 1, 0));
  for (int i = 1; i <= n; i++) {
    cin >> value;
    for (int j = 1; j <= capacity; j++)
      maxValue[i][j] = (value > j) ? (maxValue[i - 1][j]) : (max(maxValue[i - 1][j], maxValue[i - 1][j - value] + value));
  }
  cout << maxValue[n][capacity];
  return 0;
}
```

## Climbing Stairs

https://leetcode.com/problems/climbing-stairs/

```C++
class Solution {
public:
    int climbStairs(int N) {
        if (N == 1)
            return N;
        int first = 1, second = 2, next;
        while (N-- >= 3) {
            next = first + second;
            first = second;
            second = next;
        }
        return second;
    }
};
```

## Longest Increasing Subsequence

https://leetcode.com/problems/longest-increasing-subsequence/

```C++
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        int n = nums.size();
        if (n == 0)
            return 0;
        vector<int> dp(n);
        dp[0] = 1;
        int maxans = 1;
        for (int i = 1; i < n; i++) {
            int maxval = 0;
            for (int j = 0; j < i; j++)
                if (nums[i] > nums[j])
                    maxval = max(maxval, dp[j]);
            dp[i] = maxval + 1;
            maxans = max(maxans, dp[i]);
        }
        return maxans;
    }
};
```

## Coin Change

https://leetcode.com/problems/coin-change/


```C++
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        int max = amount + 1;
        vector<int> dp(max, max);
        dp[0] = 0;
        for (int i = 1; i <= amount; i++) {
            for (int j = 0; j < coins.size(); j++) {
            if (coins[j] <= i)
                dp[i] = min(dp[i], dp[i - coins[j]] + 1);
            }
        }
    return dp[amount] > amount ? -1 : dp[amount];
    }
};
```

## Coin Change 2

https://leetcode.com/problems/coin-change-2/

```C++
class Solution {
public:
    int change(int amount, vector<int>& coins) {
        int max = amount + 1;
        vector<int> dp(max);
        dp[0] = 1;
        for (int i = 0; i < coins.size(); i++)
            for (int j = coins[i]; j <= amount; j++)
                dp[j] += dp[j - coins[i]];
    return dp[amount];
    }
};
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
class Solution {
public:
    bool canJump(vector<int>& nums) {
        int lastPos = nums.size() - 1;
        for (int i = nums.size() - 1; i >= 0; i--)
            if (i + nums[i] >= lastPos)
                lastPos = i;
        return lastPos == 0;
    }
};
```

## Jump Game II

https://leetcode.com/problems/jump-game-ii/

```C++
class Solution {
public:
    int jump(vector<int>& nums) {
        if (nums.size() < 2)
            return 0;
        int ladder = nums[0];
        int stairs = nums[0];
        int jump = 1;
        for (int level = 1; level < nums.size(); level++) {
            if (level == nums.size() - 1)
                return jump;
            if (level + nums[level] > ladder)
                ladder = level + nums[level];
            stairs--;
            if (stairs == 0) {
                jump++;
                stairs = ladder - level;
            }
        }
        return jump;
    }
};
```

## Decode Ways

https://leetcode.com/problems/decode-ways/

```C++
class Solution {
public:
    int numDecodings(string s) {
        int prev = 0, cur = 1;
        for (int i = 0; i < s.length(); i++) {
            if (s[i] == '0')
                cur = 0;
            int temp = cur + prev;
            if (s[i] == '1' || s[i] == '2' && s[i + 1] <= '6')  
                prev = cur;         
            else
                prev = 0;
            cur = temp;
        }
        return cur;        
    }
};
```

## Unique Paths

https://leetcode.com/problems/unique-paths/

```C++
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<int> current(n, 1);
        for (int i = 1; i < m; i++)
            for (int j = 1; j < n; j++)
                current[j] += current[j - 1];
        return current[n - 1];
    }
};

```

## Unique Paths II

https://leetcode.com/problems/unique-paths-ii/

```C++
class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
    int width = obstacleGrid[0].size();
    vector<int>dp(width);
    dp[0] = 1;
    for (auto row : obstacleGrid) 
        for (int j = 0; j < width; j++) {
            if (row[j] == 1)
                dp[j] = 0;
            else if (j > 0)
                dp[j] += dp[j - 1];
        }
    return dp[width - 1];
    }
};
```

## Longest Common Subsequence

https://leetcode.com/problems/longest-common-subsequence/

```C++
class Solution {
public:
    int longestCommonSubsequence(string a, string b) {
        vector<vector<int>> m(a.size() + 1, vector<int>(b.size() + 1));
        for (int i = 1; i <= a.size(); i++)
            for (int j = 1; j <= b.size(); j++)
                if (a[i - 1] == b[j - 1])
                    m[i][j] = m[i - 1][j - 1] + 1;
                else 
                    m[i][j] = max(m[i - 1][j], m[i][j - 1]);
        return m[a.size()][b.size()];
    }
};
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
class Solution {
public:
    vector<vector<string>> solveNQueens(int n) {
        vector<vector<string>> res;
        vector<string> nQueens(n, string(n, '.'));
        solveNQueens(res, nQueens, 0, n);
        return res;
    }
private:
    void solveNQueens(vector<vector<string> > &res, vector<string> &nQueens, int row, int &n) {
        if (row == n) {
            res.push_back(nQueens);
            return;
        }
        for (int col = 0; col < n; col++)
            if (isValid(nQueens, row, col, n)) {
                nQueens[row][col] = 'Q';
                solveNQueens(res, nQueens, row + 1, n);
                nQueens[row][col] = '.';
            }
    }
    bool isValid(vector<string> &nQueens, int row, int col, int &n) {
        for (int i = 0; i < row; i++)
            if (nQueens[i][col] == 'Q')
                return false;
        for (int i = row - 1, j = col - 1; i >= 0 && j >= 0; i--, j--)
            if (nQueens[i][j] == 'Q')
                return false;
        for (int i = row - 1, j = col + 1; i >= 0 && j < n; i--, j++)
            if (nQueens[i][j] == 'Q')
                return false;
        return true;
    }
};
```

## N-Queens II

https://leetcode.com/problems/n-queens-ii/

```C++
class Solution {
public:
    int totalNQueens(int n) {
        int res = 0;
        vector<string> nQueens(n, string(n, '.'));
        solveNQueens(res, nQueens, 0, n);
        return res;
    }
private:
    void solveNQueens(int &res, vector<string> &nQueens, int row, int &n) {
        if (row == n) {
            res++;
            return;
        }
        for (int col = 0; col < n; col++)
            if (isValid(nQueens, row, col, n)) {
                nQueens[row][col] = 'Q';
                solveNQueens(res, nQueens, row + 1, n);
                nQueens[row][col] = '.';
            }
    }
    bool isValid(vector<string> &nQueens, int row, int col, int &n) {
        for (int i = 0; i < row; i++)
            if (nQueens[i][col] == 'Q')
                return false;
        for (int i = row - 1, j = col - 1; i >= 0 && j >= 0; i--, j--)
            if (nQueens[i][j] == 'Q')
                return false;
        for (int i = row - 1, j = col + 1; i >= 0 && j < n; i--, j++)
            if (nQueens[i][j] == 'Q')
                return false;
        return true;
    }
};
```
