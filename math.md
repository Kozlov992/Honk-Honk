# Fibonacci Number
+ [Recursion](#recursion)
+ [Bottom-Up Approach using Memoization](#bottom-up-approach-using-memoization)
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
## Bottom-Up Approach using Memoization
```C++
class Solution {
public:
    int fib(int N) {
		  if (N <= 1)
			  return N;
		  int* a = new int[N + 1];
		  int i = 2, temp = 0;
		  a[1] = 1;
		  a[0] = 0;
		  for (; i <= N; i++)
			  a[i] = a[i - 1] + a[i - 2];
		  temp = a[i - 1];
		  delete[] a;
		  return temp;
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
        int a = 0, b = 1, buf;
        while (N-- >= 2) {
            buf = a + b;
            a = b;
            b = buf;
        }
        return b;
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
