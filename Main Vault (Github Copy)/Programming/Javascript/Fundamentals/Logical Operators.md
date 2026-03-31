*Four logical operators in JS...*
```js
|| (OR)
&& (AND)
!  (NOT)
?? (Nullish Coalescing)
```

---
## <u> OR Operator </u>
*If an operand is not a boolean, it's converted to boolean for the evaluation.*

> [!tip] Boolean Conversion
> Understanding how values convert to boolean is crucial. See [[Comparisons]] for details on type conversion and truthy/falsy values.
```js
if (1 || 0){
	alert( 'Truthy!' );
}
```

> [!note] In Practice
> Logical operators are frequently used in [[Conditional Branching]] statements to combine multiple conditions and control program flow.

OR finds the first truthy value.
- Evaluates the operands from left to right.
- For each operand, converts it to boolean. If the result is `True`, stops and returns the original value of that operand.
- If all operands have been evaluated and all were `false`, returns the last operand.


> [!IMPORTANT] IMPORTANT
> A value is returned in its original form, without the conversion.


The OR operator is a short-circuit evaluation. Once a truthy value is encountered that value is returned immediately.
```js
true || alert( 'Not printed' );
false || alert( 'Printed' );
```

---

## <u> && (AND) </u>
*Returns `true` if both operands are truthy, otherwise return false.*

The && (AND) operator finds the first `falsy` value.
- Evaluates operands left to right.
- For each operand, converts it to boolean. If result is `false`, stops and returns the original value of that operand.
- If all operands have been evaluated and all were `truthy`, returns the last operand.


> [!Important] Precedence of AND `&&` is higher than OR `||`
> So the code `a && b || c && d` is essentially the same as if the `&&` expressions were in parentheses: `(a && b) || (c && d)`.

---

## <u> ! (NOT) </u>
*Converts the operand to boolean type. Returns the inverse value.*

```js
alert( !true ); //false
alert( !0 ); //true
```

a double `NOT` is sometimes used to convert a value to boolean type
```js
alert( !!"non-empty string" ); //true
alert( !!null ); //false
```

The verbose and better way to do this is to use
```js
Boolean( ... )
```

---
## <u> Nullish Coalescing Operate ?? </u>
*The nullish coalescing operator treats `null` and `undefined` as the same. 
This operator returns the first defined value (e.g. not null and or undefined)*

The result of `a ?? b:` is...
- if `a` is defined, then `a`
- if `a` is undefined/null, then `b`

```js
result = a ?? b;
result = (a != null && a != undefined) ? a : b;
//these two statements are the same.
```

The most common use case for `??` is to provide a default value to variable.
```js
let firstName = null;
let name = firstName ?? "John";
```

> [!note] Default Values
> The nullish coalescing operator is commonly used to provide default values, similar to default parameters in [[Functions]].


> [!IMPORTANT] The important difference between `??` and `||`
> `||` returns the first *truthy* value
> `??` returns the first *defined* value

heres an example...
```js
let height = 0;
alert( height || 100 ); //returns 100
alert( height ?? 100);  //returns 0
```

