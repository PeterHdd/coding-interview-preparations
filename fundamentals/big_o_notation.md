## Time and Space Complexity
----

### Big O Notation
- Big O notation: it describes how the runtime scales with respect to some input variables, where N is just a variable representing the input. If two loops are nested then you multiple, if two loops are not nested then you add the steps.
### Rules Of Big O Notation:
- Different steps get added, meaning if you have two different steps in your function then you can do *-O(a) + O(b)*
- Drop constants, meaning if you let's say two arrays then each one will take *O(N)* time to finish, you dont use *O(2N)*, you just use *O(N)*.
- Different inputs => different variables, meaning if you have two inputs in the function then you cant use O(N) only, you have to use O(a*b).
- Drop non-dominante terms, so for example if you have two steps O(n) + O(n^2), then you can just use O(n^2).

## Different Time Complexity
----

- **O(1):** Constant Time, It will always execute at the same time regardless of the size of the input data set. Example:
```
var array = [1, 2, 3, 4, 5];
array[0] // This is a constant time look-up, this will always take the same amount of time.
```
- **O(N):**  Linear Time, Describes an algorithm or program who's complexity will grow in direct proportion to the size of the input data. For example, if we have an array or list as an input and you want to find an element inside of it, then you have to iterate through all the elements to get it, which means if the list is larger, then the loop will take more time to finish, thus linear complexity.
- **O(log(n))** Logarithmic Time, Logarithm is the inverse of the exponential, for example:
```
2^3 = 8 then      => log of 8 = 3 (base 2 log of 8 is equal to 3)
10^4 = 10000 then => the base 10 log of 10000 is 4
```
Generally: if **x^z = y then logx(y) = z** The base can be any number, but in CS and in Big O we use base 2.

```
2^0 = 1        log2(1) = 0
2^1 = 2        log2(2) = 1
2^2 = 4        log2(4) = 2
2^3 = 8        log2(8) = 3
2^4 = 16       log2(16)= 4
2^5 = 32       log2(32)= 5
```
1. As you notice, each log is twice as big as the next log, but the value is only addition of (1). Binary Search which uses the divide and conquer approach has also logarithm time complexity, since as you can see if you double the data it will only require (1) extra step. Binary Search is very efficient if the data is already sorted. If you check the logarithm graph, you can see that with more time, the graph starts to level out which means it's good for big data set.

2. Logarithmic Time Complexity refers to an algorithm that runs in proportionally to the logarithm of the input size. Example:

```
var partialRange = function(array) {
  for (var i = 1; i < array.length; i = i * 2) {
    console.log(array[i]);
  }
}; //This will have a logarithmic time look-up since the function is
   //looking at only searching through part of the array.
```
The above is logarithmic since its not passing through all the elements like a linear time complexity. As you can see in the above code, `i` is multiplying by `2` so, `1,2,4,8,16,32` while the iteration is only adding `(1)` iteration in each multiplication. This can also be used with `i=i*3`

- **O(N²)** Quadratic Time, Quadratic Time Complexity represents an algorithm whose performance is directly proportional to the squared size of the input data set (think of Linear, but squared). For example nested loop, since you have to loop inside the nested for loop once and then loop again in the outer loop thus you are looping twice. Another Example:

```
 var hasDuplicates = function(array) {
  for (var i = 0; i < array.length; i++) {
    var item = array[i];
    if (array.slice(i + 1).indexOf(item) !== -1) {
      return true;
    }
  }
  return false;
}; //This will have a quadratic time look-up since the function is
  //looking at a every index in the array twice.
```
Here we loop once and then inside the if statement using `indexOf()`, we search the array again thus leading to `O(n^2)`.

- **O(2^N)** Exponential Time, Exponential Time complexity denotes an algorithm whose growth doubles with each additon to the input data set:

```
var fibonacci = function(number) {
  if (number <= 1) return number;
  return Fibonacci(number - 2) + Fibonacci(number - 1);
}; //This will have an exponential time look-up since the function 
   //is looking at a every index an exponential number of times.
```
In a few words, the recursive instantiation will pass over every number from the number to zero. It will do this twice (once for each recursive call) until it reaches the base case if statement.  

- **O(n log n)**  Linearithmic Time, This running time is often found in **divide & conquer algorithms** which divide the problem into sub problems recursively and then merge them in n time. Example: Merge Sort algorithm. Think of it as a combination of `O(logn) and O(n) => O(n*log(n))`, example:

```
for(int i = 0; i < n; i++)
  for(int j = 1; j < n; j = j * 2)
    print "hello";
```

As you can see here the inner loop will run in `O(logn)` while the outer loop will run in `O(n)`, so you multiple and get `O(n*log(n))`.

## Additional Info

##### Big-O notation
- Big-O refers to the upper bound of time or space complexity of an algorithm, meaning it worst case runtime scenario. An easy way to think of it is that runtime could be better than Big-O but it will never be worse.

##### Big-Ω (Big-Omega) notation
- Big-Omega refers to the lower bound of time or space complexity of an algorithm, meaning it is the best runtime scenario. Or runtime could worse than Big-Omega, but it will never be better.

##### Big-θ (Big-Theta) notation
- Big-Theta refers to the tight bound of time or space complexity of an algorithm. Another way to think of it is the intersection of Big-O and Big-Omega, or more simply runtime is guaranteed to be a given complexity, such as n log n.

##### What you need to know
- Big-O and Big-Theta are the most common and helpful notations
- Big-O does not mean Worst Case Scenario, Big-Theta does not mean average case, and Big-Omega does not mean Best Case Scenario. They only imply the algorithm's performance for a particular scenario, and all three can be used for any scenario.
- Worst Case means given an unideal input, Average Case means given a typical input, Best case means a ideal input. Ex. Worst case means given an input the algorithm performs particularly bad, or best case an already sorted array for a sorting algorithm.
- Best Case and Big Omega are generally not helpful since Best Cases are rare in the real world and lower bound might be very different than an upper bound.
- Big-O isn't everything. On paper merge sort is faster than quick sort, but in practice quick sort is superior.

## Time Complexity from good to bad:
- O(1)
- O(logn)
- O(n)
- O(nlogn) 
- O(n^2)
- O(2^n) 
- O(n!)

## Space Complexity
Is how many space each variable is taking, we do not count the input in space complexity, only variables inside the function.

## Calculating time complexity
- To calculate the time complexity of a program you need to only focus on the input. You can use the frequency count method.

Example 1:
```
sum(A,n)
{
    s=0; //1 unit of time
    for(i=0;i<n;i++){ //i=0 (1 time), i<n(n+1 times), i++(n times)
        s=s+A[i]; //n times, since this statement will execute for n times
        }
        return s; //execute for 1 time.
   }
```   
Result:
```
f(n) = 1 + 1 +n+1+n +n = 3n+3(remove contsants) => O(n)
```
**Note:** i<n is n+1 since in the last iteration it will check it but won't enter inside the loop therefore it is n+1.

Example 2:

```
add(A,B,n){
	for(i=0;i<n;i++){ //n+1 times
		for(j=0;j<n;j++){ //n(n+1) times
			c[i,j]=A[i,j]+B[i,j]; //n*n times
			}
		}
	}
```    

Result:
```
f(n)=n+1 + n^2 + n + n^2 = 2n^2 + 2n + 1 = O(n^2).
where A and B are matrix.
```
**Note:** the first loop is n+1 times and everything inside will iterate n times, and since there is another loop nested
then that loop will execute n+1 times and everything inside will be n times. That's why we have n(n+1).

----

**Note:** 
- if you have O(n/2) it basically means O(n) since we remove constants.
- Sum of natural numbers from 1 to n. The answer is n(n+1)/2.
- to calculate time complexity you can analyze, for example:

```
for(i=1;i<n;i=i*2)
{
    stmt
}
```
**Analyze:**
let i=1:
1
2 (1*2)
4 (2*2)
8 (2^2*2)
Therefore 2^k times.

*Assume:* `i >=n` since if i is greater than `n`, then loop will stop.
Since `i=2^k` therefore `2^k>=n => 2^k=n => k=logn`.

----

#### Recurrence Relation:

If you have a recursive call then you can use recurrence relation to get time complexity.
Recurrence relations are also of fundamental importance in analysis of algorithms. If an algorithm is designed so that it will break a problem into smaller subproblems (divide and conquer), its running time is described by a recurrence relation.
Example:
```
void test(int n){
    if(n<0){
        print("end"); //1 unit of time
        test(n-1);
    }
}
```
Assume: `T(n)` which is time taken by this algorithm.
`T(n) = T(n-1) + 2`. It's `T(n-1)` since we have `test(n-1)`.

Note: Generally speaking, an algorithm with multiple recursive calls takes exponential runtime.
So if you have `2` recursive call then its `O(2^n)`, if 3 recursive calls then `O(3^n)`.

- To get the time complexity of a recursion, we need to transform the code into a recurrence relation.
Recurrence relations are used to analyze the running time of a recursive function. The running time of a recursive function is denoted by `T(n)` where `n` is the size of the input. In recurrence relation, the running time of a recursive function of input size `n` is expressed in terms of the running time of the lower value of `n`. For example:

```
T(n)=T(n−1)+O(1) //T(n-1) + O(1) is lower than T(n) since we have -1.
```
Here, the running time for size `n` is equal to the running time for size `n−1` plus a constant time. Usually, the running time `T(n)` is expressed as a conditional statement having the following two conditions:

Base case and recursive case, example:
```
T(n)={O(1)		  if n≤2}
     {T(n−1)+O(1)         otherwise}
```
Which means when `n` is less than 2 then the solution is `O(1)`, when  it is greater than 2 then we use the recurrence relation.
Example:
```
int fact(int n) {
    if (n == 0) {
        return 1;
    }
    return n * fact(n - 1);
}
```
Here base case is `O(1)` if `n=0` therefore `T(0)=O(1)`.
Here recursive case is `T(n)=T(n-1)+O(1)` since there is only one recursive call with input size `n−1` and after the recursive function returns we do a simple multiplication that takes `O(1)`.
Therefore we get a recurrence relation:
```
T(n)={O(1)        if n=0}
     {T(n−1)+O(1) otherwise}
```

#### Solving Recurrence Relation
---
You can use the substitution method, for example:
(factorial code):

```
int factorial(int n){    
  if (n == 0)    
    return 1;    
  else    
    return(n * factorial(n-1));    
 }  
``` 
`T(n)=T(n-1)+1`, to solve it I need to find what `T(n-1)` is equal to, since `T(n)=T(n-1)+1` then `T(n-1)=T(n-1-1)+1=T(n-2)+1`, so just replace `n` with `n-1`.
```
substitute:T(n-1)

T(n)=(T(n-2)+1)+1
T(n)=T(n-2)+2
T(n)=(T(n-3)+1)+2
T(n)=T(n-3)+3
```

You can continue substituting for `k` times.
Therefore it will be `T(n)=T(n-k)+k`. Now I assume `n-k=0`,
therefore `n=k` then `T(n)=T(n-n)+n => T(0)+n => 1 + n => O(n)`.

---

Another Example:

```
void Test(int n){
	if(n>0){
		for(i=0;i<n;i++){
			print("hi");
		}
		Test(n-1);
	  }
	}
```

The recurrence relation is:
```
T(n)=T(n-1)+2n+2 => T(n) = T(n-1)+ n
```

Therefore:
```
T(n)={ 1        n=0
     { T(n-1)+n n>0
```
We can solve this using Recurrence tree method:
```
		T(n)
		/	\
		n	 T(n-1)
			  /	  \	
			n-1	    T(n-2)
					/\
				      n-2  T(n-3)
```

So basically the loop first will run `n` times, then in the next recursive call, it will run `n-1` and the call will be `T(n-2)`, then loop will run `n-2` and call will be `T(n-3)`.
We can then replace `n` by the base case which is 1. So `T(n-3)` is equal to `T(2)` until `T(0)`.
Then to find the time we check in each step how much is it:
`n + n-1 + n-2 + n-3 +.. = n(n+1)/2` (it is equal to that because here basically we are adding the summation of natural numbers
Therefore the time is `O(n^2)`.

You can also use substitution to solve it:
```
T(n)=T(n-1)+n therefore,
T(n-1)=T(n-2)+n-1. //just replace n by n-1 everywhere. and continue.
```
In the end you will get:
```
T(n)=T(n-3)+(n-2)+(n-1)+n
T(n)=T(n-k)+(n-(k-1))+(n-(k-2))+...+(n-1)+n.
```
So now assume you reached base case, so `n-k=0 => n=k`
replace `k` with `n` and you will get:
```
T(n)=T(0)+1+2+3+4..+(n-1)+n = n(n+1)/2 (summation of natural numbers).
```

----
Last Example:

```
test(int n){
    if(n>0){
        print("asd");
        test(n-1);
        test(n-1);
    }
}
```
`T(n)=2T(n-1)+1`
Recurrence Relation:
```
T(n)={1         n=0}
     {2T(n-1)+1 n>0}
```
Using substitution then:
```
T(n)=2T(n-1)+1 then T(n-1)=2T(n-2)+1
T(n)=2(2T(n-2)+1)+1
T(n)=2^2T(n-2)+2+1
T(n)=2^(2T(n-3)+1)+2+1
T(n)=2^3T(n-3)+2^2+2+1
```

Therefore:
Now replace the numbers with `k-1`
```
T(n)=2^kT(n-k)+2^(k-1)+2^(k-2)+2^2+1
```
Assume `n-k=0 =>n=k` and replace
`T(0)=2^nT(0)+1+2+2^2+...+2^k-1
=2^n=1-1 => O(2^n)`.

---

#### Master Theorem

Therefore we saw the following:
```
T(n)=T(n-1)+1 => O(n)
T(n)=T(n-1)+n => O(n^2)
T(n)=T(n-1)+logn => O(nlogn)
T(n)=2T(n-1)+1 => O(2^n)
T(n)=2T(n-1)+n => O(n2^n)
```

In the first 3 we have `a=1` where `a` is the number next to `T`.
In the last 2 we have `a>1`

We can use the master theorem formula for decreasing functions:
```
T(n)=aT(n-b)+f(n) where a>0 and b>0 and f(n) = O(n^k) where k>=0 (basically f(n) is just the time of other operations)
```

if `a=1` then `O(n^(k+1))` or `O(n*f(n))`
if `a>1` then `O((n^k)*(a^n))` //`n^k` since `f(n)` is `O(n^k)`
if `a<1` then `O(n^k)` or `O(f(n))`.

##### Master theorem for dividing functions:

Master theorem for dividing functions:
```
T(n)= aT(n/b)+f(n)
where a>=1 and b>1 and f(n)=O(n^(k)*log^(p)*n)
```

There are following three cases:

1. if `loga base b > k` then `O(n^log a base b)`
2. if `loga base b = k` then `O(n^klogn)`
3. if `loga base b < k` then `O(n^k)`

Example: 
```
T(n)=2T(n/2)+1

a=2 and b=2
f(n)=O(1) => O(n^0*log^(0)*n)  k=0 and p=0.
loga base b = log2 base 2 = 1 and k=0 therefore case 1 (in the above cases).
Answer: O(n^1) since loga base b is equal to 1.
```

Second Example:
```
T(n)=4T(n/2)+n
a=4
b=2
loga base b => log4 base 2 => 2
k=1 and p=0 therefore case 1 => O(n^2)
here k=1 since k is the power of n, so here n is power 1. If `n^2` then `k` would be equal to `2`.
```

**Note**: if f(n)=1 then O(n^0)

## Other helpful links
* [Stack Overflow: What is a plain English explanation of “Big O” notation?](http://stackoverflow.com/questions/487258/what-is-a-plain-english-explanation-of-big-o-notation?page=1&tab=votes#tab-top)

* [Big O Cheat Sheet](http://bigocheatsheet.com/)
