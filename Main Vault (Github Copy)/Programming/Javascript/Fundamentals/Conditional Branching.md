*We can use the ==if== statement and the conditional operator ==?== called question mark operator as conditional branching.

> See also: [[Comparisons]] for details on comparison operators used in conditional statements, and [[Logical Operators]] for combining multiple conditions.

## <u> Conditional Operator '?' </u>
*Sometimes, we need to assign a variable depending on a condition.*

```js
let accessAllowed;
let age = prompt('How old are you?', '');

if (age > 18){
	accessAllowed = true;
} else {
	accessAllowed = false;
}
alert( accessAllowed );
```

there is a shorted and simpler way to do this using a question mark or ternary operator.
```js
let result = condition ? value1 : value2;
```

the if statements above get converted to
```js
let accessAllowed = (age > 18) ? true : false;
```

> [!tip] Understanding Comparisons
> The `>` operator returns a boolean value. For more details on how comparison operators work and type conversion, see [[Comparisons]].

> [!important] Note:
> We can actually omit the question mark operator because the comparison itself returns true or false (see [[Comparisons]] for how JavaScript evaluates comparison operators).
> ```js
> let accessAllowed = age > 18;
> ```

---

## <u> Multiple '?' </u>
*A sequence of ? operators can return a value that depends on more than one condition.*

```js
let age = prompt('age?', 18);

let message = (age > 3) ? 'Hi, baby!' :
	(age < 18) ? 'Hello!' :
	(age < 100) ? 'Greetings!' :
	'What an unusual age!';
	
alert( message );
```
the above is equivalent to branching if statements.. shown below.

```js
if (age < 3){
	message = 'Hi, baby!';
} else if (age < 18){
	message = 'Greeings!';
} else {
	message = 'What an unusual age!';
}
```