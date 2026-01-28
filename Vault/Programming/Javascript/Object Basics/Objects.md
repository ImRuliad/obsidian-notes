*Imagine an object as a cabinet with signed files. Every piece of data is stored in its file by the key. Its easy to find a file by its name or add/remove files.*

> [!info] Working with Objects
> Objects often use dynamic property names based on user input. You can use [[Conditional Branching]] to handle different object properties, and [[Functions]] to create methods within objects.

## <u> Create Objects </u>
*An empty object can be created using one of two syntaxes*
```js
let user = new Object();    //object constructor syntax
let user = {};              //object literal syntax
```
Usually, the figure brackets `{...}` are used. That declaration is called an *object literal*

## <u> Literals and Properties </u>
*We can immediately put some properties into `{...}` as key: value pairs*
```js
let user = {
	name: "John",
	age: 30
};
```
In this object, there are two properties
- The first property `name` has the value `John`
- The second property `age` has the value `30`

We can access the property values using dot notation
```js
alert( user.name );    //John
alert( user.age );     //30
```

To remove a property, we can use `delete` operator:
```js
deleter user.age;
```

You can also use multiword property names, but they must be quoted
```js
let user = {
	name: "John",
	age: 30,
	"likes birds": true
};
```

For multiword properties, dot access doesn't work
```js
let user = {};

//set
user["likes birds"] = true;

//get
alert( user["likes birds"] );

//delete
delete user["likes birds"];
```

Square brackets also provide a way to obtain the property name as the result of any expression – as opposed to a literal string.
```js
let key = "likes birds";
user[key] = true;
```

`key` may be calculated at run-time or depend on the user input. And then we use it to access the property. That gives us a great deal of flexibility.
```js
let user = {
	name: "John",
	age: 30
};

let key = prompt("What do you want to know about the user?", "name");

alert( user[key] ); //John (if enter "name")
```

> [!Danger] Dot notation cannot be used in the same way.

## <u> Computed Properties </u>
We can use square brackets in an object literal, when creating an object. That's called a *computed properties* 
```js
let fruit = prompt("Which fruit to buy?", "apple");

let bag = {
	[fruit]: 5,
};
alert( bag.apple );
```
The meaning of a *computed property* `[fruit]` means that the property name should be. taken from `fruit`.
So, if a visitor enters `"apple"`, `bag`  will become `{apple: 5}`.

This basically works the same as
```js
let fruit = prompt("Which fruit to buy?", "apple");
let bag = {};

bag[fruit] = 5;
```

We can use more complex expressions inside square brackets
```js
let fruit = 'apple':
let bag = {
	[fruit + 'Computers']: 5    //bag.appleComputers = 5
};
```

> [!Important] When property names are known and simple use dot notation. If something more complex is needed, then use square brackets!
