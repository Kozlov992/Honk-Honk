# Fibonacci Number
+ [Recursion](#recursion)
+ [Recursive Approach using Memoization](#recursive-approach-using-memoization)
+ [Iterative Top-Down Approach](#iterative-top-down-approach)
+ [Binet's formula](#binet's-formula)
https://leetcode.com/problems/fibonacci-number/

## Recursion
```C++
class Solution {
public:
    int fib(int N) {
        if (N <= 1)
            return N;
        else
            return fib(N - 1) + fib(N - 2);
    }
};
```
## Recursive Approach using Memoization
```C++
class Solution {
public:
    int fib(int N) {
        if (N <= 1)
            return N;
        int memo[N + 1] = {0, 1};
        return fib(N, memo);        
    }
    int fib(int N, int* memo){
        if (N <= 1)
            return N;
        if (!memo[N])
            memo[N]= fib(N - 1, memo) + fib(N - 2, memo);
        return memo[N];
    }
};
```
## Iterative Top-Down Approach
```C++
class Solution {
public:
    int fib(int N) {
        if (N <= 1)
            return N;
        int first = 0, second = 1, next;
        while (N-- >= 2) {
            next = first + second;
            first = second;
            second = next;
        }
        return second;
    }
};
```
## Binet's formula
```C++
class Solution {
public:
    int fib(int N) {
        return round(pow((1+sqrt(5)) / 2, N)/sqrt(5));
    }
};
```
