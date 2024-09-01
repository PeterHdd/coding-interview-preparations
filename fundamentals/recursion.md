# Recursion
Recursion is when a function calls itself. This requires at least O(n) memory usage for the stack storing the function calls. [Here](https://www.youtube.com/watch?v=k0bb7UYy0pY) is a great explanation of stack usage in recursive functions.

### Code Example

<details>
<summary> Java Implementation of Recursion </summary>

```java
public class Factorial {

    public static void main(String[] args) {
        int num = 6;
        long factorial = multiplyNumbers(num);
        System.out.println("Factorial of " + num + " = " + factorial);
    }

    public static long multiplyNumbers(int num)
    {
        if (num >= 1)
            return num * multiplyNumbers(num - 1);
        else
            return 1;
    }
}
```
</details>

<details>
<summary>Python Implementation of Recursion</summary>

```python
# Python 3 program to find 
# factorial of given number 
def factorial(n): 
	
	# Checking the number
	# is 1 or 0 then
	# return 1
	# other wise return
	# factorial
	if (n==1 or n==0):
		
		return 1
	
	else:
		
		return (n * factorial(n - 1)) 

# Driver Code 
num = 5; 
print("number : ",num)
print("Factorial : ",factorial(num))
```
</details>

------

- You can use memoization with recursion (check dynamic programming section).
- Example of Recursion:
```java
int fun(n){
if(n==1) return 1;
else return 1 + fun(n-1);
}
```

- So basically first the `main()` method will be added to the stack by the operating system, containing all the local fields.
- Then inside the `main()` we call the function `fun()` which makes the function `main()` the caller function of the function `fun(3)`.
- So `fun(3)` will be added in the stack, then since we are calling it again with different parameter therefore we add `fun(2)` in the stack above `fun(3)`. So now `fun(3)` is the caller of `fun(2)`, then we do the same and add `fun(1)` above `fun(2)`. and now since we reached the base case which is `if(n == 1) return 1`. Therefore we check in `fun(1)` if it satisfies the condition which is done, therefore it returns 1 to the caller which is `fun(2)`. So here we remove `fun(1)` from the stack, return 1, and `fun(2)` continues where it stops. So `fun(2)` will become:
```java
int fun(2){
if(n==1) return 1;
else return 1 + fun(1) => else return 1 + 1;
```
- So now `2` will be returned to the caller which is `fun(3)` and `fun(2)` will be removed from stack. So in `fun(2)` we replace it will 2 and do 2+1 = 3, so `fun(3)` will be popped from the stack and return 3 to it's caller which is `main()`. Reference: https://www.youtube.com/watch?v=kepBmgvWNDw&ab_channel=NesoAcademy

## Tail Recursion
A recursive function is tail recursive when recursive call is the last thing executed by the function. Tail recursion is where calculations are performed first and then the recursive call is executed. Some programming languages, usually functional ones, optimize tail calls so they take up less room on the call stack. 

