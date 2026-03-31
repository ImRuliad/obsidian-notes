
## <u> For Loops </u>
*This is an inline variable declaration...*
```js
for (let i = 0; i < 3; ++i) {
	alert(i); //0, 1, 2
}
```

*instead of defining a variable, we can use an existing one...
we can also skip parts of the for loop*
```js
let i = 0;
for (; i < 3; i++) {
	alert(i); //0, 1, 2
}
```

*you can also remove the step part*
```js
let i = 0;

for (; i < 3;) {
	alert(i++);
}
//identical to while (i < 3)
```

> [!note] Loop Conditions
> Loop conditions use [[Comparisons]] operators to determine when to continue or exit the loop. Complex conditions can be built using [[Logical Operators]] to combine multiple conditions. See also [[Conditional Branching]] for related control flow patterns.

---
## <u> Breaking the Loop </u>
*Normally a loop exits when the condition becomes falsy.
We can force the exit of a loop using the `break` directive.*

```js
let sum = 0;
while (true) {
	let value = +prompt("Enter a number", '');
	
	if (!value) break;
	sum += value;
}
alert( "Sum: ${sum}");
```

You can't use `break` or `continue` to the right side of `?`
for example, if we take this code...
```js
if (i > 5) {
	alert(i);
} else {
	continue;
}
```
and rewrite it using...
```js
(i > 5) ? alert(i) : continue;
```
it would stop working, its a syntax error.

---
## <u> Labels for break and continue </u>
*sometimes we need to break out from multiple nested loops at once.*
```js
for (let i = 0; i < 3; ++i) {
	for (let j = 0; j < 3; ++j) {
		let input = prompt("Value at coords: (${i}, ${j})", '');
		
		//what if we want to exit from here to Done (below) ?
	}
}
alert('Done!');
```
here, the ordinary `break` after the `input` would only break the inner loop. What if we want to break out of all loops at once?

*A label is an identifier with a colon before a loop*
```js
labelName: for (...) {
	...
}
```

using `break <labelName>` statement in the loop below breaks out to the label:
```js
outer: 
for (let i = 0; i < 3; ++i) {
	for (let j = 0; j < 3; ++j) {
		let input = prompt("Value at coords: (${i}, ${j})", '');
		
		//if an empty string or cancelled, then break out of both loops
		if (!input) break outer;
		
		//do something with the value.
	}
}
alert( 'Done!' );
```


> [!Important] Break and Continue is only possible within loops.
> ...
