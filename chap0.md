## Chapter 01. Understanding recursion 

Recursion is the fundamental concept that is needed to understand Dynamic programming. 
Dynamic programming is an algorithm design technique. 
This design technique is easy to understand. 
You break a big problem into small subproblems which are easy to solve. Then you solve these 
subproblems. When solving the subproblems, these solutions for the sub problems should eventually solve the 
ultimate problem you are trying to solve. To optimize this process we use memorization. Which means for every
subproblem that we solve, we store the solution, and then if we encounter a similar problem, we use the stored 
solution, instead of recomputing everything from scratch. This allows for great speed ups in time complexity. 

To understand dynamic programming, we need to understand how to do basic recursion. 
A helloworld application of recursion is the fibonacci sequence. 
How does that work? 

The fibonacci sequence works as follows, 
if the position of the number is n, then then fibonacci of n is the fibonacci of n-1 and the fibonacci of n-2. 

```javascript 
fib(n) = fib(n-1) + fib(n-2) 
```


Therefore to solve fib(n) we must know the fib of (n-1) and fib of (n-2). Which are sub problems. Therefore we can apply 
Dynamic programming to solve this function. 

How? 
We write a recursive function as below to solve this problem. It is a basic recursion function. 
Every recursive function has one key attribute: a base case. 
A base case is how the recursive function knows when to stop. Here if the input is less than or equal to 2, we return 
1. This is the base case. If there wasn't a base case the function would go on forever calling itself and never complete. 

```javascript 
function fib(n){
  if (n <= 2) return 1; 
  return fib(n-1) + fib(n-2); 
}
```
We can think of recursive functions as tree graphs. This is how I got my understanding of recursion. 
This was a hard concept to grasp at first, because our minds are not designed to think in a recursive manner, it is not natural!

Therefore we must need to visualize this using a graph. 
Let's see the example for a fib of 10. 
This would be the graph. 
![fib graph](https://github.com/oysters76/DP/blob/main/IMG_20210111_230445.jpg)
The calling function, or the root function (fib(10)) would call two functions fib(9) and fib(8). The function splits here and the 
tree graph is created. Likewise the child elements split into two until a base condition is met. Then the tree stops splitting and the 
results are bubbled upwards. Finally the results reach fib(10) node and the user gets the output of the function. 

However the time complexity of this function is exponential. Which is not a problem for small values of n, but once the values 
exceed even a small amout (e.g. 50) the function gets slow. To overcome this we use memorization. This means, by using a hashmap 
(key value dataset), we can map the problem with a solution, and reuse the solution in recurring problems. This would ensure we 
would never recalculate the same problem over and over again. 

Here is a memorization based fibonacci solver 
```javascript 
function fib(n, memo={}){
  if (n in memo) return memo[n]; 
  if (n <= 2) return 1; 
  memo[n] = fib(n-1,memo) + fib(n-2,memo); 
  return memo[n]; 
}
```

This is a break down of the fib(5) tree 
![fib graph](https://github.com/oysters76/DP/blob/main/IMG_20210114_222416.jpg)

notice that the fib(5) can be expressed as 
```
fib(5) = fib(2) + fib(1) + fib(2) + fib(1) + fib(2) 
```
