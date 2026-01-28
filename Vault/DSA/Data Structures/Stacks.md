# What is a Stack?
## A stack is a data structured referred to as a *collection*.
- ##### It operates in a *LIFO (Last In First Out)* manner.
## What makes a stack unique is that:
- ##### You can only add to or remove from one point.
- ##### Where you add and remove from are the same point in the stack.

# Think of Stacks like a stack of plates at a restaurant.
- #### When we initialize a stack it is empty. 
- #### When we first add to the stack it is placed at the bottom.
- #### Subsequent additions to the stack are added on top of the stack.

# In a stack structure there is *no* way to access arbitrary elements in the stack.
### You can only access the top item using *peak*.
- #### You can theoretically access lower items in the stack by popping the higher items first.
- #### This is inefficient and defeats purpose of stack.

# Purpose of a Stack
---
## Stacks are good for
- ### When we need adding and or removing often.
- ### When we need data to be ordered in a recursive fashion.

# How to Initialize a Stack
``` 
import java.util.Stack; // This references the Stack class of the Java API
Stack<String> st = new Stack<>(); // Declared and initializes empty string stack 
st.push(“String #1”); // Add first string to stack  
st.push(“String #2”); // Add second string to stack  
String s = st.pop(); // Capture removed item into string “s”  
String s2 = st.peek(); // Save string at top of stack into string “s2”  
boolean b = st.isEmpty(); // Saves whether stack is empty (it isn’t currently so this is false) int n = st.size(); // Save number of items in stack in “n”  
st.clear(); // Resets stack to empty
```