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
        string word1, word2;
        unsigned int len;
        for (int i = 1; i < words.size(); i++){
            word1 = words[i];
            word2 = words[i - 1];
            (word1.length() <= word2.length()) ? (len = word1.length()) : (len = word2.length());
            for (int j = 0 ; j < len; j++){
                if (word1[j] != word2[j]) {
                    graph[word1[j] - 'a'].push_back(word2[j] - 'a');
                    break;
                }
            }
        }
        return graph;
    }
    bool DFS(const vector<vector<int>>& graph, vector<bool>& ActualLetters, vector<bool>& CompletedLetters, int letter, string& alphabet){
        if (CompletedLetters[letter]){
            return true;
        }
        int numb = 0;
        ActualLetters[letter] = true;
        for (auto i : graph[letter]) {
            if (!CompletedLetters[i]){
                if (ActualLetters[i]){
                    return false;
                }
                if (DFS(graph, ActualLetters, CompletedLetters, i, alphabet)){
                    CompletedLetters[i] = true;
                }
            }
            if (CompletedLetters[i]){
                numb++;
            }
        }
        alphabet.push_back('a' + letter);
        if (numb == graph[letter].size()){
            return CompletedLetters[letter] = true;
        }
        return false;
        
    }
    string alienOrder(vector<string> &words) {
        vector<bool> letters('z' - 'a' + 1, false);
        string alphabet;
        vector<vector<int>> graph = BuildGraph(words);
        vector<bool> CompletedLetters('z' - 'a' + 1, false);
        for (auto word : words){
            for(auto letter : word){
                letters[letter - 'a'] = true;
            }
        }
        for (int i = 0; i < graph.size(); i++) {
            vector<bool> ActualLetters('z' - 'a' + 1, false);
            if (!CompletedLetters[i] && letters[i]){
                if (!DFS(graph, ActualLetters, CompletedLetters, i, alphabet)) {
                    return "";
                }
            }
        }
        return alphabet;
    }
};
```
