# Arrays

+ [Two Sum](#two-sum)
+ [Three Sum](#three-sum)
+ [Sum Equals K](#sum-equals-k)

## Two Sum 

https://leetcode.com/problems/two-sum/

1)No auxiliary space
```C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        for (int i = 0; i < nums.size(); i++){
            for (int j = i + 1; j < nums.size(); j++){
                if (nums[j] == target - nums[i])
                    return vector<int> {i, j};
            }
        }
        return  vector<int> (0);
    }
};
```
2)Using map

```C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target)  {
        map<int, int> Sum;
        for (int i = 0; i < nums.size(); i++) {
            int secondNum = target - nums[i];
            if (Sum.find(secondNum) != Sum.end())           
                return vector<int> {i, Sum[secondNum]}; 
            Sum[nums[i]] = i;
        }
        return vector<int> (0);
    }
};
```
    
## Three Sum

https://leetcode.com/problems/3sum/

```C++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
      vector<vector<int>> result(0);
      sort(nums.begin(), nums.end());
      int size = nums.size();
      for (int i = 0; i < size - 2; i++) {    
        int left = i + 1;
        int right = size - 1;
        while (right > left) {      
            int sum = nums[i] + nums[left] + nums[right];
            if (sum > 0)
                right--;
            else if (sum < 0)
                left++;
            else {
                vector<int> subArr = {nums[i], nums[left], nums[right]};
                result.push_back(subArr);
                while (left < right && nums[left] == subArr[1])
                    left++;
                while (left < right && nums[right] == subArr[2])
                    right--;
            }
        }
        while (i < size - 2 && nums[i] == nums[i + 1])
            i++;
      }
      return result;
    }
};
```

## Sum Equals K

https://leetcode.com/problems/subarray-sum-equals-k/

1)No auxiliary space
```C++
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        int count = 0;
        for (int begin = 0; begin < nums.size(); begin++) {
            int sum = 0;
            for (int end = begin; end < nums.size(); end++) {
                sum += nums[end];
                if (sum == k)
                    count++;
            }
        }
        return count;
    }
};
```

2)Using map

```C++
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        int count = 0;
        map<int, int> cSum;
        cSum[0]++;
        int sum = 0;
        for (int i = 0; i < nums.size(); i++) {
            sum += nums[i];
            count += cSum[sum - k];
            cSum[sum]++;
        }
        return count;
    }
};
```
