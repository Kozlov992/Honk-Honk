# Intervals

+ [Non-overlapping Intervals](#non-overlapping-intervals)
+ [Merge Intervals](#merge-intervals)
+ [Insert Interval](#insert-interval)

## Non-overlapping Intervals

https://leetcode.com/problems/non-overlapping-intervals/

```C++
class Solution {
public:
    int eraseOverlapIntervals(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end());
        int count = 0, prev = 0;
        for (int i = 1; i < intervals.size(); i++) {
            if (intervals[i][0] < intervals[prev][1]) {
                count++;
                if (intervals[i][1] < intervals[prev][1])
                    prev = i;
            }
            else
                prev = i;
        }
    return count;
    }
};
```

## Merge Intervals

https://leetcode.com/problems/merge-intervals/

```C++
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end());
        vector<vector<int>> merged(0);
        if (intervals.size() != 0)
            merged.push_back(intervals[0]);
        for (int i = 1; i < intervals.size(); i++) {
            if (merged.back()[1] < intervals[i][0])
                merged.push_back(intervals[i]);
            else
                merged.back()[1] = max(merged.back()[1], intervals[i][1]);
        }
    return merged;
    }
};
```

## Insert Interval

https://leetcode.com/problems/insert-interval/

```C++
class Solution {
private:
    vector<vector<int>> mergeSorted(vector<vector<int>>& intervals) {
        vector<vector<int>> merged(0);
        if (intervals.size() != 0)
            merged.push_back(intervals[0]);
        for (int i = 1; i < intervals.size(); i++) {
            if (merged.back()[1] < intervals[i][0])
                merged.push_back(intervals[i]);
            else
                merged.back()[1] = max(merged.back()[1], intervals[i][1]);
        }
    return merged;
    }
public:
    vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
        if (intervals.size() == 0)
            return vector<vector<int>> {newInterval};
        for (int i = 0; i < intervals.size(); i++) {
            if (intervals[i][0] > newInterval[0]) {
                intervals.insert(intervals.begin() + i, newInterval);
                break;
            }
            if (i == intervals.size() - 1) {
                intervals.push_back(newInterval);
                break;
            }
        }
        return mergeSorted(intervals);
    }
};
```
