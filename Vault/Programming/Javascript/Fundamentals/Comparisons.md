Here are some examples of comparisons. Comparisons are commonly used in [[Conditional Branching]] statements.
```javascript
alert(2 > 1); //true
alert(2 == 1); //false
alert(2 != 1); //true
```

comparisons can also be assigned to a variable
```javascript
let result = 5 > 4; //true
alert(result); 
```

---
## <u> String Comparison </u>
*To see whether a string is greater than another, JS uses "dictionary" or "lexicographical" order.*
*Strings are compared letter by letter.*
```javascript
alert( 'Z' > 'A' );       //true
alert( 'Glow' > 'Glee' ); //true
alert( 'Bee' > 'Be' );    //true
```

The algorithm to compare two strings is simple:
1. Compare the first character of both strings.
2. If the character from the first string is greater than (or less than) the character from the second then we're done.
3. Otherwise, if both strings' first characters are the same, compare the second characters the same way as above.
4. Repeat until the end of either string.
5. If both strings end at the same length, then they are equal. Otherwise, the longer string is greater.

---
## <u> Comparison of Different Types </u>
*When comparing values of different types, Javascript converts the values to numbers.*

for example
```js
alert( '2' > 1); //true '2' becomes 2
alert( '01' == 1); //true '01' becomes 1
```
*for boolean values, true becomes 1 and false becomes 0.*

> [!note] In Practice
> This boolean-to-number conversion is particularly important when writing [[Conditional Branching]] statements, where comparisons evaluate to boolean values that control program flow.

---
## <u> Strict Equality </u>
 *A regular equality only checks equality between values, not types.*
 *Strict equality operator checks the equality without the type conversion.*
 ```js
 alert( 0 == false ); //true
 alert( '' == false ); //true
 ```
this happens because operands of different types are converted to numbers by the equality operator ==

```js
alert( 0 === false); //false because the types are different.
```

> [!tip] When to Use Strict Equality
> Use `===` (strict equality) in [[Conditional Branching]] to avoid unexpected type conversion behavior.

---

## <u> Comparison with Null and Undefined </u>
```js
alert( null === undefined ); //false
alert( null == undefined );  //true
```
null and undefined are converted to numbers
- null becomes 0.
- undefined becomes NaN.