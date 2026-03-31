*Arrow functions are essentially more concise versions of [[Function Expressions|Function Expressions]]*

> [!note] Related Topics
> Arrow functions are a modern alternative to traditional [[Functions|function declarations]] and [[Function Expressions]]. They provide a shorter syntax and have different `this` binding behavior.

here's what it looks like...
```js
let func = (arg1, arg2, ..., argN) => expression;
```
*This creates a function `func` that accepts arguments `arg1 .. argN`, then evaluates the `expression` on the right hand side with their use and returns its results.*

This is essentially a shorter version of...
```js
let func = function(arg1, arg2, ..., argN) {
	return expression;
}; n
```

Here's a better example...
```js
let sum = (a, b) => a + b;
alert( sum(1,2) );    //3
```

If we only have one argument, then we can omit the parenthesis...
```js
let double = n => n*2;
alert( double(3) );    //6
```

If there are no arguments, then the parenthesis are empty, but they must be present...
```js
let sayHi = () => "Say Hi!";
sayHi();    //Say Hi!
```

## <u> Multiline Arrow Functions </u>
*Multiline arrow functions can be expressed with a curly braces `{ .. }` to the right of the `=>`*
*Multiline arrow functions require a `return` statement within them.*

```js
let sum = (a, b) => {
	let result = a + b;
	return result;
};

alert( sum (1,2) );
```