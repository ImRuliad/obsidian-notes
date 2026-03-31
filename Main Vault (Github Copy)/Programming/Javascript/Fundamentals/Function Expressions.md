
## This is a [[Functions#<u> Function Declaration </u>|Function Declaration]]
```js
function sayHi() {
	alert( "Hello" );
}
```

## This is a Function Expression
```js
let sayHi = function() {
	alert( "Hello" );
};
```
*Function Expressions allow us to create a new function in the middle of any expression.*
*Its called a function expression because the function is defined on the right side of the `=`.

> [!Important] Important
> Function Expressions have a semicolon at the end.
> 
> 

These are essentially the same
```js
function sayHi() {
	alert( "Hello" );
}
let func = sayHi;
func();    //Hello
sayHi();   //Hello
```

```js
let sayHi = function() {
	alert( "Hello" );
};
let func = sayHi;
```

---

## <u> Callback Functions </u>
*Imagine a function `ask(question, yes, no)` with three parameters*
- `Question` - text of the question
- `yes` - function to run if answer is yes
- `no` - function to run if answer is no

this function should ask the `question` and call `yes()` or `no()` depending on the user's answer.
```js
function ask(question, yes, no) {
	if (confirm(question)) {
		yes()
	} else {
		no()
	}
}

function showOk() {
	alert( "You said YES." );
}

function showCancel() {
	alert( "You said NO." );
}

ask("Do you agree?", showOk, showCancel);
```

We can use Function Expressions to write an equivalent, shorter function..
```js
function ask(question, yes, no) {
	if (confirm(question)) {
		yes()
	} else {
		no()
	}
}

ask(
	"Do you agree?",
	function() { alert( "You said YES." ); },
	function() { alert( "You said NO." ); }
);
```
*Functions are declared right inside the `ask(...)` call. They have no name, and are called `Anonymous` functions. These functions are not accessible outside of `ask(...)` because they are not assigned to variables.*



> [!Important] Difference between Function Declaration and Function Expression
> ***<u>A Function Expression is created when the execution reaches it and is usable only from that moment. </u>***
> 
> Once the execution flow passes to the right side of the assignment `let sum = function(){...};` then the function is created and can be used from now on.
> 
> *** <u>A Function Declaration can be called earlier than it is defined. </u> ***
> 
> A global function declaration is visible in the whole script, no matter where it is. When JavaScript prepares to run the script, it first looks for global Function Declarations in it and creates the functions. After all Function Declarations are processed, the code is executed.

---
## <u> More Differences </u>
*When a Function Declaration is within a code block, it's visible everywhere inside that block, but not outside of it.*
```js
let age = prompt( "What is your age?", 18);

if (age < 18) {
	function welcome() { alert( "Hello!" ); }
} else {
	function welcome() { alert( "Greetings!" ); }
}

welcome();    /// Error: welcome is not defined.
```

What can we do to make `welcome` visible outside of `if` ?
we can use a Function Expression.
```js
let age = prompt( "What is your age?", 18);
let welcome;

if (age < 18) {
	welcome = function() { alert ( "Hello!" ); };
} else {
	welcome = function() { alert ( "Hello!" ); };
}

welcome();    //ok now.
```

we can simplify it even further using [[Conditional Branching#<u> Conditional Operator '?' </u>|Question Mark Operator ?]]
```js
let age = prompt("What is your age?", 18);

let welcome = (age < 18) ?
	function() { alert( "Hello!" ); } :
	function() { alert( "Greetings!" ); };
	
welcome();    //this is ok now.
```


> [!Important] When to choose Function Declaration versus Function Expression
> When we need to declare a function, the first thing to consider is Function Declaration syntax. It gives more freedom in how to organize code because we can call these functions before they are declared.
>
> But if a Function Declaration does not suit us for some reason, or we need a conditional declaration, then Function Expression should be used.
>
> For even more concise syntax, consider using [[Arrow Functions]], which are a shorter form of Function Expressions with some differences in `this` binding.

