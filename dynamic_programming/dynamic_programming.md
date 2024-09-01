#### Dynamic Programming
#### Definition
- Dynamic programming is when you use past knowledge to make solving a future problem easier.
- Dynamic programming is used a lot in string problems, such as the string edit problem. You solve a subset(s) of the problem and then use that information to solve the more difficult original problem.
- Dynamic programming is a technique used to avoid computing multiple times the same subproblem in a recursive algorithm.
#### What you need to know (https://stackoverflow.com/a/18342131/7015400)
- With dynamic programming, you store your results in some sort of table generally. When you need the answer to a problem, you reference the table and see if you already know what it is. If not, you use the data in your table to give yourself a stepping stone towards the answer.
- Memoization is a term describing an optimization technique where you cache previously computed results, and return the cached result when the same computation is needed again.
- Dynamic programming is a technique for solving problems of recursive nature, iteratively and is applicable when the computations of the subproblems overlap.
- Dynamic programming is typically implemented using tabulation, but can also be implemented using memoization. So as you can see, neither one is a "subset" of the other.
- Dynamic Programming is often called Memoization
- On a basic level Dynamic programming is recursion + memoization(cache)
- DP finds the solution by starting from the base case(s) and works its way upwards. DP solves all the sub-problems, because it does it bottom-up (start solving from the trivial sub-problem, up towards the given problem).
- By using memoization, the time complexity will become less, and memoization is often called top down approach (start solving the given problem by breaking it down)
- Memoization ensures that method does not execute more than once for same inputs by storing the results in the data structure(Usually Hashtable or HashMap or Array).

Example Fibonacci using Memoization (top down):

<details>
<summary> Java Implementation</summary>

```java
public class FibonacciMemoizationAlgorithm {
 
 private Map<Integer, Integer> memoizeTable = new HashMap<>(); // O(1)
 
 // Fibonacci with Memoization
 public int fibonacciMemoize(int n){
 
 if( n == 0 ) return 0;
 if( n == 1 ) return 1;
 
 if( this.memoizeTable.containsKey(n) ) 
 {
 System.out.println("Getting value from computed result for "+n);
 return this.memoizeTable.get(n);
 }
 
 int result = fibonacciMemoize(n-1)+ fibonacciMemoize(n-2);
 
 System.out.println("Putting result in cache for "+n);
 this.memoizeTable.put(n, result);
 
 return result;
 
 }
 
 // Fibonacci without Memoization
 public int fibonacci(int n){
 
 if( n == 0 ) return 0;
 if( n == 1 ) return 1;
 
 System.out.println("Calculating fibonacci number for: "+n);
 return (fibonacci(n-1) + fibonacci(n-2)); 
 }
 
 public static void main(String[] args) {
 
 FibonacciMemoizationAlgorithm fibonacciAlgorithm = new FibonacciMemoizationAlgorithm();
 System.out.println("Fibonacci value for n=5:  "+fibonacciAlgorithm.fibonacciMemoize(5));
 
 }
}
 ```

</details>

<details>
<summary> Python Implementation </summary>

```python
class FibonacciMemoizationAlgorithm:
    def __init__(self):
        self.memoize_table = {}  # O(1)

    def fibonacci_memoize(self, n):
        if n == 0:
            return 0
        if n == 1:
            return 1

        if n in self.memoize_table:
            print(f"Getting value from computed result for {n}")
            return self.memoize_table[n]

        result = self.fibonacci_memoize(n - 1) + self.fibonacci_memoize(n - 2)

        print(f"Putting result in cache for {n}")
        self.memoize_table[n] = result

        return result

fib = FibonacciMemoizationAlgorithm()
result = fib.fibonacci_memoize(10)
print(f"Fibonacci(10) = {result}")
```
</details>

## Example of Dynamic programming:

```
int fib(int n){
int A[];
A[0]=0; A[1]=1;
for(int i=2;i<=n;i++){
A[i] = A[i-1] + A[i-2];
}
return A[n];
}
```
Basically this will create an array that will contain 0 and 1, then in the loop we start from the 2nd index, so A[2]=A[2-1]+A[2-2]=A[1]+A[0]=1+0=1 so in this case we start from bottom while in memoization we start from the top.