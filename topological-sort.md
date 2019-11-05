# Topological sort

+ [Course Schedule](#course-schedule)
+ [Course Schedule II](#course-schedule-ii)
+ [Alien Dictionary](#alien-dictionary)

## Course Schedule
https://leetcode.com/problems/course-schedule/
``` C++
class Solution {
public:
    bool isCycled(const vector<vector<int>>& graph, vector<bool>& visiting, vector<bool>& visited, int node){
        if (visiting[node])
            return true;
        if (visited[node])
            return false;
        visiting[node] = true;
        for (auto i : graph[node])
            if (isCycled(graph, visiting, visited, i))
                return true;
        visiting[node] = false;
        visited[node] = true;
        return false;
        
    }
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        vector<vector<int>> graph(numCourses);
        vector<bool> visiting(numCourses,false);
        vector<bool> visited(numCourses,false);
        for (int i = 0; i < prerequisites.size(); i++)
          graph[prerequisites[i][0]].push_back(prerequisites[i][1]);
        for (int node = 0; node < numCourses; node++)
            if (isCycled(graph, visiting, visited, node))
                return false;
        return true;
        
    }
};
```

## Course Schedule II
https://leetcode.com/problems/course-schedule-ii/
``` C++
class Solution {
public:
    bool isCycled(const vector<vector<int>>& graph, vector<bool>& visiting, vector<bool>& visited, int node, vector<int>& result){
        if (visiting[node])
            return true;
        if (visited[node])
            return false;
        visiting[node] = true;
        for (auto i : graph[node])
            if (isCycled(graph, visiting, visited, i, result))
                return true;
        visiting[node] = false;
        visited[node] = true;
        result.push_back(node);
        return false;
        
    }
    vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
        vector<vector<int>> graph(numCourses);
        vector<bool> visiting(numCourses,false);
        vector<bool> visited(numCourses,false);
        vector<int> result(0);
        for (int i = 0; i < prerequisites.size(); i++)
          graph[prerequisites[i][0]].push_back(prerequisites[i][1]);
        for (int node = 0; node < numCourses; node++)
            if (isCycled(graph, visiting, visited, node, result))
                return {};
        return result;
    }
};
```
## Alien Dictionary
https://www.lintcode.com/problem/alien-dictionary/description
``` C++

```
