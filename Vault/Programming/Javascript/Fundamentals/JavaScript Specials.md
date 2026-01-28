*Subtle moments about everything in Fundamentals.*

> [!info] Overview
> This document summarizes key JavaScript concepts covered in the Fundamentals section. For detailed information, see: [[Conditional Branching]], [[Comparisons]], [[Logical Operators]], [[Functions]], [[Function Expressions]], [[Arrow Functions]], and [[While and For Loops]].

## <u> Variables </u>
- `let`
	- Block scoped (limited to nearest curly brace)
	- Can be reassigned new values even in the same scope.
	- Can't re-declaration in the same scope.
- `const`
	- Block scoped (limited to nearest curly brace)
	- Cannot be reassigned.
	- Can't re-declaration in the same scope.
- `var`
	- Function scoped(or globally scoped if declared outside a function). 
	- Can be reassigned new values even in the same scope.
	- Allows re-declaration in the same scope.


> [!Important] Best Practice
> Use `const` by default, `let` when you need reassignment, and avoid `var` since `let` and `const` provide more predictable scoping behavior.

| Data Type | Definition                                                      |
| --------- | --------------------------------------------------------------- |
| number    | Floating point numbers & integer numbers                        |
| bigint    | For integer numbers of arbitrary length                         |
| string    | For strings                                                     |
| boolean   | Logical values `true` and `false`                               |
| null      | A type with a single `null` meaning "empty" or "does not exist" |
| undefined | A type with a single value `undefined` meaning "not assigned"   |
| object    | For complex data structures and unique identifiers.             |
| symbol    | For complex data structures and unique identifiers.             |

---

## <u> Interaction </u>
`prompt(question, [default])`
- Ask a `question`, and return either what the user entered or `null` if they clicked cancel.
`confirm(question)`
- Ask a `question` and suggest to choose between Ok and Cancel. Returned as `true` or `false`
`alert(message)`
- Output a `message`

