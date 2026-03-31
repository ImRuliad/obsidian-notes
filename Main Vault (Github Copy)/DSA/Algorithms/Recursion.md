# What is Recursion?
---
## Recursion allows us to achieve a form of looping by exploiting the program stack. Stacks are naturally recursive data structures.

### Recursion is when a method calls itself. All forms of looping (iteratively or recursively), must contain three properties:
- #### Starting Condition
- #### Step Condition
		- #### Ending Condition
##### The initial call of a recursive method is its starting position, its ending condition is a conditional statement in the recursive method that prevents a Stack Overflow. Everything else in between is a Step Condition.

# Stack Overflow vs Infinite Loop
---
## Why Do Stack Overflows Happen?
### Stack Overflows happen because a function or method call does not have a step condition within it. The result is that the method continues to call itself, placing more methods on the program stack without popping anything. Once the number of methods exceeds the stack bound a Stack Overflow occurs.

```
// Inside main method...  
int max = 10;  
recurse(max);

// The recurse wrapper method 
public static void recurse(int max){
	recurse_helper(0, max); 
}

// The recurse helper method  
public static void recurse_helper(int i, int max){
	if(i > max) 
		return;
	System.out.println(i);  
	recurse_helper(++i, max);
```
## Why Do Infinite Loops Happen?
##### Infinite Loops happen because a method or function does not have a step condition properly implemented within it. It continues to loop and loop infinitely in an iterative fashion.
```
int i = 0;

while(i < 10){
	System.out.println(i); 
}
```
## Whats the difference?
##### *Stack overflow* deals with methods or functions calling itself so much so that the amount of methods in the program stack exceeds the Stack bound resulting in a stack overflow error.

##### *Infinite Loops* occur because a function or method itself does not have a step condition properly implemented within itself. The function/method loops indefinitely within itself without end.

# Due to the overhead associated with method calls on the program stack, it is faster to use iterative versions of loops.
##### (In some cases it is easier to use recursion such as with Binary Tree Traversal because of its recursive tree structure Left-Middle-Right for InOrder)

# Efficiency vs Inefficiency
---
### The classic recursive solution for fibonacci sequence works but is inefficient
```
public static int fib(int n){
	if(n <= 1)
		return n;
	return fib(n-1) + fib(n-2);
}
```
### The method above is redundant and works in exponential time algorithm. Here is a iterative solution in linear time.
```
public static int fib(int n){
	int n1 = 0;
	int n2 = 0;
	int n3 = 1;
	for(int i = 1; i < n; i++){
		n1 = n2;
		n2 = n3;
		n3 = n1+n2;
	}
	return n3;
}
```
### You can turn convert iterative solutions into recursive ones although, you will sacrifice readability in favor of shorter code.
```
public static int fib(int n, int n1, int n2, int n3, int i){
	if (i == n)
		return n3;
	return fib(n, n2, n3, n2+n3, i+1)
}
```
### So the solution is to use Wrapper / Helper methods
```
private static int fib(int n, int n1, int n2, int n3, int i){
	if(i == n)
		return n3;
	return fib(n, n2, n3, n2+n3, i+1);
}
public static int fib(int n){
	return fib(n, 0, 0, 1, 1);
}
```
