*Quite often we need to perform a similar action in many places of the script.
For example, we need to show a nice-looking message when a visitor logs in, logs out and maybe somewhere else.
Functions are the main "building blocks" of the program. They allow the code to be called many times without repetition.*

> [!info] Related Function Topics
> See also: [[Function Expressions]] for alternative function syntax, and [[Arrow Functions]] for a more concise modern syntax.

## <u> Function Declaration </u>

heres a basic function
```js
function showMessage() {
	alert( 'Hello everyone!' );
}
```

---

## <u> Local Variables </u>
*A variable declared inside a function is only visible inside that function.*
```js
function showMessage() {
	let message = "Hello, user!";
	alert( message );
}

showMessage();     // Hello, user!
alert( message );  // Error! The variable is local to the func.
```

---
## <u> Outer Variables </u>
*A function can access an outer variable as well.*
```js
let userName = 'John';

function showMessage() {
	let message = "Hello, ${userName}!";
	alert( message ); 
}
showMessage(); //Hello, John
```

*what happens if we modify this variable?*
```js
let userName = 'John';

function showMessage() {
	userName = 'Bob';
	let message = "Hello, ${userName}!";
	alert(message);
}
alert( userName ); //John -> the function has not executed yet and hasn't changed the value of userName
showMessage();
alert( userName ); //Bob -> the function has now executed and has changed the value of userName
```

*if the same variable is declared again inside the function, then it shadows the outer one.*
```js
let userName = 'John';

function showMessage() {
	userName = 'Bob';
	let message = "Hello, ${userName}!";
	alert(message);
}

showMessage();        //Hello, Bob!
alert( userName );    //John
```

---

## <u> Parameters </u>
*We can pass arbitrary data to function using parameters*
- ***Parameter*** - the variable listed inside the parentheses in the function declaration.
- ***Argument*** - the value that is passed to the function when it's called.

*If a function is called, but an argument is not provided, then the corresponding value becomes `undefined`.
We can specify the so-called default value for a parameter in the function declaration using `=`*
```js
function showMessage(from, text="no text given!"){
	alert( "${from} : ${text}" );
}
showMessage("Ann"); //Ann: no text given
```


> [!IMPORTANT] A function with an empty `return` or with a `return` returns `undefined`
> if a function does not return a value, it is the same as if it returns `undefined`...
> ```js
> function doNothing() { /* empty */ }
> alert( doNothing() === undefined ); //true
> ```
>
> an empty `return` is also the same as `return undefined`
> ```js
> function doNothing() {
> 	return;
> }
> alert ( doNothing() === undefined ); //true
> ```
>
> See [[Comparisons]] for more details on comparing with `undefined` and using strict equality (`===`).

