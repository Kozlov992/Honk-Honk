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
class Solution {
public:
    vector<vector<int>> BuildGraph(vector<string> &words){
        vector<vector<int>> graph('z' - 'a' + 1);
        for (int i = 0; i < words.size() - 1; i++){
            string word1 = words[i];
            string word2 = words[i + 1];
            unsigned int len = max(word1.length(), word2.length());
            for (int j = 0 ; j < len; j++){
                if (word1[j] != word2[j]) {
                    graph[word1[j] - 'a'].push_back(word2[j] - 'a');
                    break;
                }
            }
        }
        return graph;
    }
    bool DFS(const vector<vector<int>>& graph, vector<bool>& visiting, vector<bool>& visited, int letter, string& alphabet){
        if (visiting[letter])
            return true;
        if (visited[letter])
            return false;
        visiting[letter] = true;
        for (auto i : graph[letter])
            if (DFS(graph, visiting, visited, i, alphabet))
                return true;
        visiting[letter] = false;
        visited[letter] = true;
        alphabet.insert(alphabet.begin(), letter + 'a');
        return false;
        
    }
    string alienOrder(vector<string> &words) {
        vector<bool> visiting('z' - 'a' + 1,false);
        vector<bool> visited('z' - 'a' + 1, false);
        vector<bool> letters('z' - 'a' + 1, false);
        string alphabet;
        vector<vector<int>> graph = BuildGraph(words);
        for (auto word : words){
            for(auto letter : word){
                letters[letter - 'a'] = true;
            }
        }
        for (int i = graph.size() - 1; i >= 0; i--) {
            if (letters[i] && DFS(graph, visiting, visited, i, alphabet))
                return "";
        }
        return alphabet;
    }
```
