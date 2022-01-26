# Functions

1. Functions in Javascript are objects.
2. Objects are collections of name/value pairs having hidden link to a prototype object.
3. Functions objects are linked to **Function.prototype** which is itself linked to **Object.prototype**
4. Functions can be stored in variables, objects, and arrays. Functions can be passed as arguments to functions, and functions can be returned from functions. Also, since functions are objects, functions can have methods.
5. Every function is also created with two additional hidden properties: the function’s context and the code that implements the function’s behavior.
6. Every function object is also created with a prototype property. Its value is an object with a constructor property whose value is the function. This is distinct from the hidden link to Function.prototype

__## Function Literal__

1. Functions can be defined inside of other functions. An inner function, of course, has access to its parameters and variables. An inner function also enjoys access to the parameters and variables of the functions it is nested within.
The function object created by a function literal contains a link to that outer context. This is called **closure**

